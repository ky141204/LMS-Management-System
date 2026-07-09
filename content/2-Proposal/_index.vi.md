---
title: "Đề xuất"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

## Triển khai Web LMS-Management-System trên AWS với AWS Amplify, Amazon EC2, Amazon DocumentDB và mô hình phân tán

### 1. Tóm tắt đề tài

Đề tài đề xuất triển khai hệ thống **LMS-Management-System** trên AWS theo mô hình phân tán, phù hợp cho việc quản lý học viên, khóa học, bài học, tiến độ học tập và tài khoản quản trị. Người dùng truy cập hệ thống thông qua tên miền được quản lý bởi Cloudflare. Phần giao diện được triển khai bằng AWS Amplify, trong khi các API nghiệp vụ được xử lý qua Application Load Balancer và các máy chủ EC2 chạy trong Auto Scaling Group.

Hệ thống sử dụng Amazon DocumentDB làm cơ sở dữ liệu chính để lưu dữ liệu dạng document như thông tin người dùng, khóa học, bài giảng, bài nộp và trạng thái học tập. Database được triển khai trong private subnet và hỗ trợ Multi-AZ replication để tăng tính sẵn sàng. Các thành phần giám sát gồm Amazon CloudWatch, CloudWatch Alarm và Amazon SNS để gửi cảnh báo qua email khi hệ thống có bất thường.

### 2. Vấn đề cần giải quyết

#### Vấn đề hiện tại

Các hệ thống LMS nhỏ thường được triển khai trên một máy chủ duy nhất, dẫn đến nhiều rủi ro:

- Khi lượng truy cập tăng, máy chủ dễ quá tải.
- Nếu máy chủ hoặc cơ sở dữ liệu gặp sự cố, toàn bộ hệ thống có thể bị gián đoạn.
- Việc giám sát log, metric và cảnh báo chưa được tự động hóa.
- Chứng chỉ HTTPS, DNS và bảo mật thường được cấu hình thủ công, khó duy trì lâu dài.
- Dữ liệu học tập như tiến độ khóa học, bài nộp và lịch sử hoạt động cần được lưu trữ ổn định, dễ mở rộng.

#### Giải pháp đề xuất

Giải pháp sử dụng kiến trúc cloud-native trên AWS để tách riêng các lớp frontend, backend, database và monitoring. Cloudflare đảm nhận DNS và bảo vệ lớp truy cập ban đầu. AWS Amplify lưu trữ frontend và tích hợp SSL/TLS thông qua AWS Certificate Manager. Backend LMS chạy trên EC2 phía sau Application Load Balancer, có Auto Scaling Group để tự động mở rộng khi tải tăng. Amazon DocumentDB được đặt trong private subnet để hạn chế truy cập trực tiếp từ Internet và phù hợp với dữ liệu dạng document của LMS.

#### Lợi ích kỳ vọng

- Tăng độ sẵn sàng nhờ triển khai đa Availability Zone.
- Tự động mở rộng backend bằng Auto Scaling Group.
- Bảo mật tốt hơn nhờ tách public subnet và private subnet.
- Có khả năng giám sát, cảnh báo và gửi email tự động.
- Kiến trúc có thể mở rộng cho các tính năng LMS như quản lý khóa học, lớp học, bài giảng, tiến độ học tập, bài nộp và tài khoản người dùng.

### 3. Kiến trúc giải pháp

Kiến trúc tổng thể của hệ thống được mô tả như sau:

![Kiến trúc Web LMS trên AWS](images/1.png)

Luồng xử lý chính:

1. Người dùng gửi HTTPS request đến tên miền của hệ thống.
2. Cloudflare xử lý DNS và chuyển hướng request đến hạ tầng AWS.
3. AWS Amplify phục vụ frontend và sử dụng SSL/TLS certificate từ AWS Certificate Manager.
4. Các API request được chuyển đến Application Load Balancer.
5. ALB phân phối request đến các EC2 instance trong public subnet.
6. EC2 đọc và ghi dữ liệu LMS vào Amazon DocumentDB trong private subnet.
7. DocumentDB replication giữa hai Availability Zone giúp tăng tính sẵn sàng dữ liệu.
8. EC2 gửi metric và log đến Amazon CloudWatch.
9. CloudWatch Alarm kích hoạt cảnh báo khi có lỗi hoặc vượt ngưỡng tài nguyên.
10. Amazon SNS gửi email notification cho người quản trị.

#### Các dịch vụ AWS sử dụng

- **AWS Amplify**: Triển khai và hosting frontend.
- **AWS Certificate Manager**: Quản lý SSL/TLS certificate cho HTTPS.
- **Amazon VPC**: Tạo môi trường mạng riêng cho hệ thống.
- **Internet Gateway**: Cho phép public subnet kết nối Internet.
- **Application Load Balancer**: Phân phối traffic đến các EC2 instance.
- **Amazon EC2**: Chạy backend application/API.
- **Auto Scaling Group**: Tự động tăng hoặc giảm số lượng EC2 instance theo tải.
- **Amazon DocumentDB**: Lưu trữ dữ liệu dạng document trong private subnet.
- **Amazon CloudWatch**: Thu thập log và metric của hệ thống.
- **CloudWatch Alarm**: Kích hoạt cảnh báo khi hệ thống có dấu hiệu bất thường.
- **Amazon SNS**: Gửi thông báo qua email cho người quản trị.
- **Cloudflare**: Quản lý DNS, tăng tốc và bảo vệ lớp truy cập bên ngoài AWS.

#### Thiết kế thành phần

- **Giao diện người dùng**: Website được build và deploy trên AWS Amplify.
- **DNS và HTTPS**: Cloudflare quản lý DNS; AWS Certificate Manager cấp chứng chỉ SSL/TLS.
- **Backend**: EC2 instance xử lý API và nghiệp vụ LMS như khóa học, bài học, người dùng, tiến độ học tập và bài nộp.
- **Cơ sở dữ liệu**: Amazon DocumentDB lưu dữ liệu LMS trong private subnet, không public trực tiếp ra Internet.
- **Tính sẵn sàng cao**: Hệ thống triển khai trên hai Availability Zone để giảm rủi ro downtime.
- **Giám sát hệ thống**: CloudWatch thu thập metric/log; CloudWatch Alarm và SNS gửi cảnh báo qua email.

### 4. Kế hoạch triển khai kỹ thuật

#### Các giai đoạn triển khai

- **Giai đoạn 1 - Nghiên cứu và thiết kế kiến trúc**: Tìm hiểu yêu cầu hệ thống, xác định các dịch vụ AWS cần dùng và hoàn thiện sơ đồ kiến trúc.
- **Giai đoạn 2 - Thiết lập mạng và bảo mật**: Tạo VPC, public/private subnet, Internet Gateway, security group và cấu hình DNS/HTTPS.
- **Giai đoạn 3 - Triển khai ứng dụng**: Deploy frontend lên AWS Amplify, triển khai backend trên EC2 và đặt EC2 phía sau ALB.
- **Giai đoạn 4 - Cơ sở dữ liệu và replication**: Tạo Amazon DocumentDB trong private subnet và cấu hình replication giữa hai Availability Zone.
- **Giai đoạn 5 - Giám sát và thông báo**: Thiết lập CloudWatch metric/log, CloudWatch Alarm, SNS topic và email notification.
- **Giai đoạn 6 - Kiểm thử và tối ưu**: Kiểm thử truy cập HTTPS, API, database, scaling, failover và cảnh báo.

#### Yêu cầu kỹ thuật

- Có kiến thức cơ bản về AWS VPC, subnet, security group và routing.
- Biết triển khai ứng dụng frontend bằng AWS Amplify.
- Biết cấu hình EC2, ALB và Auto Scaling Group.
- Hiểu cách kết nối backend với Amazon DocumentDB.
- Biết sử dụng CloudWatch, CloudWatch Alarm và Amazon SNS để giám sát hệ thống.
- Sử dụng Cloudflare để quản lý DNS và trỏ domain đến hệ thống.

### 5. Lộ trình và cột mốc

- **Tuần 1-2**: Phân tích yêu cầu, nghiên cứu kiến trúc và chuẩn bị tài liệu thiết kế.
- **Tuần 3-4**: Xây dựng VPC, subnet, routing, security group và cấu hình DNS.
- **Tuần 5-6**: Deploy frontend trên AWS Amplify và cấu hình SSL/TLS.
- **Tuần 7-8**: Triển khai backend trên EC2, cấu hình ALB và Auto Scaling Group.
- **Tuần 9-10**: Tạo DocumentDB, kết nối backend với database và kiểm thử dữ liệu.
- **Tuần 11**: Thiết lập CloudWatch, Alarm, SNS và email notification.
- **Tuần 12**: Kiểm thử toàn bộ hệ thống, tối ưu chi phí và hoàn thiện báo cáo.

### 6. Ước tính chi phí

Chi phí dưới đây là ước tính cho môi trường demo/thực tập, giả định triển khai tại region **US East (N. Virginia)**, traffic thấp, dữ liệu nhỏ và chưa bao gồm thuế. Khi triển khai thực tế cần kiểm tra lại bằng **AWS Pricing Calculator** vì giá có thể thay đổi theo region, cấu hình instance và mức sử dụng.

| Dịch vụ | Cấu hình giả định | Cách tính tham khảo | Chi phí/tháng ước tính |
|---|---:|---:|---:|
| AWS Amplify Hosting | 300 phút build, 1 GB lưu trữ, 10 GB data out | Build + lưu trữ + truyền dữ liệu | $4.52 |
| Amazon EC2 | 2 instance nhỏ cho backend LMS | 2 instance chạy 730 giờ/tháng | $15.18 |
| Amazon EBS | 2 volume 20 GB cho EC2 | 40 GB/tháng | $3.20 |
| Application Load Balancer | 1 ALB, traffic thấp | Phí theo giờ của ALB + LCU thấp | $18.20 |
| Amazon DocumentDB | Serverless/demo, 0.5 DCU tối thiểu, 10 GB lưu trữ | DCU-hour + lưu trữ | $31.00 |
| Amazon CloudWatch | Log, metric và alarm cơ bản | Log ingestion + alarm | $2.00 |
| Amazon SNS | Email notification số lượng thấp | Notification cơ bản | $0.10 |
| AWS Certificate Manager | Public SSL/TLS certificate | Không tính phí cho public certificate dùng với dịch vụ AWS | $0.00 |
| Data Transfer | Dưới mức free tier 100 GB/tháng | Lưu lượng outbound thấp | $0.00 |
| **Tổng cộng** |  |  | **$74.20/tháng** |
| **Ước tính 12 tháng** |  |  | **$890.40/năm** |

Đối với môi trường production có DocumentDB cluster nhiều instance, traffic cao hoặc lưu trữ nhiều dữ liệu học tập, chi phí sẽ tăng đáng kể. Trong giai đoạn thực tập, hệ thống nên dùng cấu hình nhỏ, giới hạn traffic thử nghiệm, cleanup tài nguyên không dùng và bật AWS Budget để tránh vượt chi phí.

### 7. Đánh giá rủi ro

#### Ma trận rủi ro

- **Traffic tăng đột biến**: Mức ảnh hưởng cao, khả năng xảy ra trung bình.
- **EC2 instance lỗi**: Mức ảnh hưởng trung bình, khả năng xảy ra trung bình.
- **Database quá tải hoặc lỗi replication**: Mức ảnh hưởng cao, khả năng xảy ra thấp.
- **Cấu hình security group sai**: Mức ảnh hưởng cao, khả năng xảy ra trung bình.
- **Chi phí vượt dự kiến**: Mức ảnh hưởng trung bình, khả năng xảy ra trung bình.

#### Chiến lược giảm thiểu

- Sử dụng Auto Scaling Group để tự động mở rộng backend.
- Triển khai nhiều Availability Zone để giảm rủi ro gián đoạn.
- Đặt DocumentDB trong private subnet và giới hạn inbound rule.
- Bật CloudWatch Alarm cho CPU, memory, request lỗi và trạng thái instance.
- Thiết lập AWS Budget và theo dõi chi phí định kỳ.

#### Kế hoạch dự phòng

- Nếu EC2 lỗi, Auto Scaling Group tạo instance mới thay thế.
- Nếu backend quá tải, tăng instance type hoặc điều chỉnh scaling policy.
- Nếu database gặp sự cố, kiểm tra replica và backup trước khi khôi phục.
- Nếu chi phí tăng bất thường, tạm giảm tài nguyên không cần thiết và kiểm tra log traffic.

### 8. Kết quả kỳ vọng

#### Cải thiện về kỹ thuật

- Website có HTTPS, DNS rõ ràng và frontend được deploy tự động.
- Backend có khả năng mở rộng qua ALB và Auto Scaling Group.
- Database được bảo vệ trong private subnet và hỗ trợ Multi-AZ replication.
- Hệ thống có giám sát metric/log và cảnh báo qua email.

#### Giá trị lâu dài

Kiến trúc này có thể tiếp tục mở rộng cho hệ thống LMS thực tế, bổ sung các chức năng như authentication, phân quyền giảng viên/học viên, quản lý lớp học, upload tài liệu, bài kiểm tra, notification, CI/CD và backup tự động. Đây cũng là nền tảng tốt để thực hành các chủ đề AWS quan trọng trong quá trình thực tập.
