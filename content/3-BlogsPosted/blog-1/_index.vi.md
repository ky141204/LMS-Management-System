---
title: "Blog 1"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Xây dựng hệ thống cấu hình đa đối tượng thuê với các mẫu lưu trữ được gắn thẻ
---

> [!IMPORTANT]
> ### 🎯 Mục tiêu bài viết
> Trong các kiến trúc microservices hiện đại, quản lý cấu hình đa đối tượng thuê (multi-tenant configuration) vẫn là một trong những thách thức vận hành lớn nhất. Bài viết này hướng dẫn chi tiết cách thiết kế một dịch vụ cấu hình hiệu năng cao, bảo mật và hướng sự kiện trên nền tảng AWS, giải quyết triệt để nút thắt cổ chai về cache TTL và đồng bộ dữ liệu theo thời gian thực.
> 
> *   **Bài viết gốc đăng tải tại:** [AWS Study Group](https://awsstudygroup.com/2026/05/14/xay-dung-he-thong-cau-hinh-da-doi-tuong-thue-voi-cac-mau-luu-tru-duoc-gan-the/)

---

## 1. Thách thức lớn của Hệ thống Cấu hình Đa đối tượng thuê

Khi các tổ chức mở rộng quy mô hệ thống SaaS (Software as a Service) lên đến hàng trăm hoặc hàng nghìn đối tượng thuê (tenants), các kiến trúc quản lý cấu hình truyền thống thường bộc lộ hai khoảng trống lớn:

1.  **Độ trễ khi vô hiệu hóa cache (Cache Invalidation TTL)**: 
    *   Siêu dữ liệu đối tượng thuê thay đổi nhanh hơn mức TTL của cache cho phép.
    *   Các chiến lược caching truyền thống buộc phải đánh đổi: chấp nhận ngữ cảnh đối tượng thuê cũ (rò rỉ dữ liệu hoặc cờ tính năng không chính xác) hoặc vô hiệu hóa cache liên tục làm tăng tải cho dịch vụ siêu dữ liệu.
2.  **Sự đánh đổi về Backend lưu trữ (Storage Backend Mismatch)**:
    *   Các loại cấu hình khác nhau có mẫu truy cập rất khác nhau.
    *   Cấu hình đối tượng thuê thay đổi liên tục yêu cầu tần suất đọc/ghi cực cao phù hợp với **Amazon DynamoDB**.
    *   Các cấu hình hệ thống chung hoặc cài đặt phân cấp cần được lập phiên bản thì phù hợp với **AWS Systems Manager Parameter Store**.
    *   Sử dụng một backend duy nhất cho tất cả các loại cấu hình sẽ làm giảm đáng kể hiệu năng vận hành.

---

## 2. Giải pháp: Mẫu lưu trữ được gắn thẻ (Tagged Storage Pattern)

Phương pháp này sử dụng tiền tố khóa cấu hình (ví dụ: `tenant_config_` hoặc `param_config_`) để tự động định tuyến các yêu cầu cấu hình đến dịch vụ lưu trữ AWS phù hợp nhất thông qua thiết kế **Config Strategy Factory**.

![Kiến trúc tổng thể hệ thống cấu hình đa đối tượng thuê trên AWS](images/multi_tenant_architecture.png)

### Sơ đồ luồng hoạt động (End-to-End Workflow)
Dựa trên sơ đồ kiến trúc tổng thể, luồng xử lý yêu cầu và cập nhật diễn ra thông qua 13 bước chặt chẽ:

1.  **Xác thực người dùng**: Client/Apps gửi yêu cầu đăng nhập đầu tiên tới **Amazon Cognito** `(1)`.
2.  **Trả về JWT Token**: **Amazon Cognito** xác thực thông tin và trả về JWT Token chứa thuộc tính đối tượng thuê tùy chỉnh (`custom:tenantId`) `(2)`.
3.  **Gửi yêu cầu API**: Client thực hiện các yêu cầu REST kèm theo JWT Token đi qua **AWS WAF** bảo vệ `(3)`.
4.  **Định tuyến API Gateway**: Yêu cầu đi tiếp vào **AWS API Gateway (Public REST API)** `(4)`.
5.  **Tích hợp riêng tư**: Sử dụng **VPC Link V2** để tích hợp an toàn `(5)` định tuyến traffic vào mạng nội bộ VPC.
6.  **Định tuyến tải**: **Application Load Balancer** nhận request và phân phối tới **REST API Controller** của **Order Service** chạy trên ECS Fargate `(6)`.
7.  **Tra cứu dịch vụ**: **Order Service** thực hiện DNS Lookup qua **AWS Cloud Map** `(7)` để tìm địa chỉ của Config Service (`config-service.local:5000`).
8.  **Gọi gRPC**: **gRPC Client** bên trong Order Service thiết lập kết nối và gọi hàm `(8)` sang **gRPC Controller** của **Config Service** giúp tối ưu băng thông.
9.  **Định tuyến chiến lược**: **Config Strategy Factory** `(9)` phân tích tiền tố của cấu hình yêu cầu:
    *   Nếu có tiền tố `tenant_config_*` $\rightarrow$ Chọn **DynamoDB Strategy** truy xuất qua Gateway Endpoint với khóa phân vùng `TENANT#{tenantId}`.
    *   Nếu có tiền tố `param_config_*` $\rightarrow$ Chọn **SSM Strategy** truy xuất qua Interface Endpoint từ **Parameter Store** (được mã hóa bởi AWS KMS).
10. **Bắt sự kiện thay đổi**: Khi có sự thay đổi cấu hình trên Parameter Store, một sự kiện thay đổi `(10)` được gửi tới **Amazon EventBridge**.
11. **Kích hoạt Lambda**: **Amazon EventBridge** phát hiện sự kiện và kích hoạt (Trigger) `(11)` hàm **AWS Lambda**.
12. **Truy vấn DNS & Làm mới cache**: **AWS Lambda** tra cứu dịch vụ qua Cloud Map `(12)` và thực hiện gọi hàm `gRPC refresh() Direct` `(13)` trực tiếp đến Config Service để xóa bỏ hoặc làm mới cache cục bộ ngay lập tức mà không cần khởi động lại container.

---

## 3. Các thành phần và Lớp kiến trúc cốt lõi

Hệ thống được tổ chức thành 4 lớp liên kết chặt chẽ để tối ưu hóa hiệu năng và bảo mật:

### 💼 Lớp 1: Lớp lưu trữ – Chiến lược Đa Backend (Multi-Backend Storage)
*   **Amazon DynamoDB (Cấu hình riêng biệt của Tenant)**:
    *   Lưu trữ các cấu hình mang tính duy nhất của từng khách hàng (cổng thanh toán, cờ tính năng).
    *   Sử dụng lược đồ khóa tổng hợp: Khóa phân vùng `TENANT#{tenantId}`, Khóa sắp xếp `CONFIG#{configType}` giúp cô lập dữ liệu tuyệt đối ở cấp độ model.
    *   Độ trễ truy xuất chỉ một chữ số mili giây (single-digit millisecond).
*   **AWS Systems Manager Parameter Store (Cấu hình dùng chung)**:
    *   Quản lý các thông số tương đối tĩnh nhưng mang tính phân cấp (API endpoints, Connection String).
    *   Cấu trúc đường dẫn dạng `/config-service/{tenantId}/{service}/{parameter}` hỗ trợ truy xuất hàng loạt (Batch get), giảm số lượng API calls từ hàng chục xuống chỉ còn một yêu cầu duy nhất khi khởi tạo.

### 🔌 Lớp 2: Lớp dịch vụ – gRPC kết hợp Pattern Strategy
*   Sử dụng framework **NestJS** kết hợp giao thức **gRPC** hiệu năng cao cho giao tiếp nội bộ giữa các microservices (East-West traffic). 
*   **Pattern Strategy** giúp tách biệt logic nghiệp vụ khỏi phần triển khai lưu trữ thực tế, cho phép dễ dàng mở rộng thêm các kho lưu trữ mới (ví dụ S3 đối với các file cấu hình kích thước lớn) mà không cần cấu trúc lại toàn bộ mã nguồn lõi.

### 🔐 Lớp 3: Lớp xác thực – Trích xuất ngữ cảnh từ Cognito JWT Claims
*   Cognito thiết lập các thuộc tính tùy chỉnh bắt buộc:
    *   `custom:tenantId` (bất biến) – ID của đối tượng thuê.
    *   `custom:role` (có thể thay đổi) – Vai trò của người dùng.
*   **Thiết kế an toàn**: Dịch vụ cấu hình tuyệt đối không nhận tham số `tenantId` truyền trực tiếp từ client API parameters. Thay vào đó, nó giải mã JWT Token từ API Gateway chuyển tiếp để trích xuất `custom:tenantId`, ngăn chặn hoàn toàn lỗ hổng IDOR (Insecure Direct Object Reference) và nguy cơ rò rỉ chéo dữ liệu giữa các tenants.

### ⚡ Lớp 4: Lớp làm mới theo sự kiện (Event-Driven Refresh)
Giải pháp giải quyết triệt để nút thắt cổ chai của cache TTL truyền thống thông qua cơ chế tự động cập nhật hướng sự kiện:
*   Tránh việc thăm dò (Polling) liên tục gây tốn chi phí gọi API và tạo độ trễ thông tin.
*   Tránh việc khởi động lại dịch vụ làm gián đoạn phiên kết nối của người dùng (Zero downtime).
*   Sử dụng bộ đôi **Amazon EventBridge** + **AWS Lambda** để bắt sự kiện cập nhật cấu hình của Parameter Store và đẩy trực tiếp tín hiệu xóa cache tới API gRPC của Config Service, thời gian đồng bộ cache trên toàn cụm server ECS diễn ra chỉ trong vài giây.

---
> [!TIP]
> ### 💡 Tóm tắt giá trị kiến trúc mang lại
> *   **Cô lập đa đối tượng thuê tuyệt đối**: Bảo mật từ tầng xác thực Cognito JWT claim đến phân vùng lưu trữ DynamoDB.
> *   **Hiệu năng vượt trội**: Kết hợp linh hoạt sức mạnh của gRPC cùng định tuyến Strategy thông minh cho từng loại backend.
> *   **Zero-Downtime**: Cơ chế làm mới cache hướng sự kiện qua Event Bridge loại bỏ hoàn toàn việc restart dịch vụ khi có cập nhật cấu hình mới.
