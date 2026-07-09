---
title: "Blog 2"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Kết nối an toàn AWS DevOps Agent với các dịch vụ riêng tư trong VPC của bạn
---

> [!IMPORTANT]
> ### 🎯 Mục tiêu bài viết
> Bài viết này hướng dẫn cách thiết lập **kết nối riêng tư (Private Connection)** giúp **AWS DevOps Agent** truy cập an toàn vào các dịch vụ nội bộ chạy bên trong Amazon VPC mà không cần phơi bày chúng ra internet công cộng — giải quyết triệt để rào cản bảo mật khi tích hợp các MCP server, công cụ quan sát tự host và hệ thống kiểm soát mã nguồn doanh nghiệp.
>
> *   **Bài viết gốc đăng tải tại:** [AWS Study Group](https://awsstudygroup.com/2026/04/20/ket-noi-an-toan-aws-devops-agent-voi-cac-dich-vu-rieng-tu-trong-vpc-cua-ban/)

---

## 1. Giới thiệu về AWS DevOps Agent

**AWS DevOps Agent** là đồng đội vận hành luôn sẵn sàng, được thiết kế để:

*   Giải quyết và **chủ động ngăn chặn sự cố** hệ thống trước khi chúng xảy ra.
*   **Tối ưu hóa độ tin cậy và hiệu suất** ứng dụng theo thời gian thực.
*   Xử lý các tác vụ **SRE (Site Reliability Engineering)** theo yêu cầu trên môi trường AWS, đa đám mây và tại chỗ (on-premises).
*   Tích hợp với các công cụ quan sát (Observability) hiện có để tương quan dữ liệu đo từ xa, mã nguồn và lịch sử triển khai — từ đó **giảm MTTR (Mean Time To Repair)** đáng kể.

Nhiều tổ chức mở rộng **AWS DevOps Agent** với các công cụ **Model Context Protocol (MCP)** tùy chỉnh, cho phép Agent truy cập các hệ thống nội bộ như:
*   Các kho gói riêng tư (Private Package Repositories).
*   Nền tảng quan sát tự host như Grafana, Splunk.
*   API tài liệu nội bộ.
*   Hệ thống kiểm soát mã nguồn như **GitHub Enterprise** và **GitLab**.

Vấn đề đặt ra là các dịch vụ này thường chạy bên trong **Amazon VPC** mà **không có quyền truy cập internet công cộng**, khiến AWS DevOps Agent không thể truy cập chúng theo mặc định.

---

## 2. Giải pháp: Kết nối riêng tư (Private Connection)

**Kết nối riêng tư** cho AWS DevOps Agent cho phép bạn kết nối an toàn **Agent Space** của mình với các dịch vụ đang chạy trong VPC hoặc mạng nội bộ, mà **không cần phơi bày chúng ra internet công cộng**.

Kết nối riêng tư hoạt động với bất kỳ tích hợp nào cần truy cập một endpoint riêng tư, bao gồm:
*   Các **MCP Server** tùy chỉnh.
*   Các phiên bản **Grafana hoặc Splunk** tự host.
*   Các hệ thống **kiểm soát mã nguồn** nội bộ.

### Cơ chế hoạt động

Về cơ bản, AWS DevOps Agent sử dụng **Amazon VPC Lattice** để thiết lập đường dẫn kết nối an toàn và riêng tư này. VPC Lattice là một dịch vụ mạng ứng dụng cho phép bạn kết nối, bảo mật và giám sát giao tiếp giữa các ứng dụng trên các VPC, tài khoản và loại tính toán khác nhau mà **không cần quản lý cơ sở hạ tầng mạng cơ bản**.

Khi bạn tạo một kết nối riêng tư, quá trình diễn ra theo thứ tự:

1.  Bạn cung cấp **VPC, các Subnet** và (tùy chọn) các **Security Group** có kết nối mạng đến dịch vụ đích.
2.  AWS DevOps Agent tạo một **Resource Gateway** được quản lý bởi dịch vụ và cấp phát các **Elastic Network Interfaces (ENIs)** trong các Subnet bạn đã chỉ định.
3.  Agent sử dụng Resource Gateway để **định tuyến lưu lượng** đến địa chỉ IP hoặc tên DNS của dịch vụ đích qua đường dẫn mạng riêng tư.

> Resource Gateway được AWS DevOps Agent quản lý hoàn toàn và xuất hiện dưới dạng **tài nguyên chỉ đọc** trong tài khoản của bạn. Bạn không cần cấu hình hoặc duy trì nó. Các ENI **không chấp nhận kết nối đến từ internet** và bạn giữ toàn quyền kiểm soát lưu lượng thông qua Security Group của riêng mình.

---

## 3. Kiến trúc tổng thể

![Kiến trúc kết nối riêng tư AWS DevOps Agent với VPC](images/devops_agent_private_connection.png)

### Luồng hoạt động (End-to-End Flow)

| Bước | Thành phần | Mô tả |
| :---: | :--- | :--- |
| **①** | **AWS DevOps Agent → Amazon VPC Lattice** | Agent khởi tạo yêu cầu, định tuyến qua VPC Lattice. |
| **②** | **Amazon VPC Lattice → Resource Gateway** | VPC Lattice chuyển tiếp yêu cầu đến Resource Gateway được quản lý bởi dịch vụ nằm trong Customer VPC. |
| **③** | **Resource Gateway → ENI (qua IP/DNS)** | Resource Gateway phân phối lưu lượng tới các ENI trong Resource Gateway Subnet thông qua địa chỉ IP hoặc tên DNS. |
| **④** | **ENI → Application (nội bộ hoặc On-Premises)** | ENI chuyển tiếp yêu cầu đến Application đích bên trong VPC hoặc Customer Private Network, được bảo vệ bởi Security Group. |

*Từ góc độ của dịch vụ đích, yêu cầu bắt nguồn từ **địa chỉ IP riêng tư của ENI** trong VPC — hoàn toàn không lộ ra internet công cộng.*

---

## 4. Các lớp bảo mật

> [!TIP]
> ### 🔐 Bảo mật đa lớp (Defense in Depth)
>
> Kết nối riêng tư được thiết kế với **4 lớp bảo vệ** chặt chẽ:
>
> 1.  **Không phơi bày ra internet công cộng**: Toàn bộ lưu lượng truy cập giữa AWS DevOps Agent và dịch vụ đích đều nằm trên **mạng nội bộ AWS**. Dịch vụ của bạn không bao giờ cần địa chỉ IP công cộng hoặc Internet Gateway.
> 2.  **Resource Gateway chỉ đọc, kiểm soát bởi dịch vụ**: Resource Gateway là chỉ đọc trong tài khoản của bạn. Nó **chỉ có thể được sử dụng bởi AWS DevOps Agent**, không có dịch vụ hoặc principal nào khác có thể định tuyến lưu lượng qua nó. Mọi hành động đều được ghi lại đầy đủ trong **AWS CloudTrail**.
> 3.  **Security Group hoàn toàn do bạn kiểm soát**: Lưu lượng từ DevOps Agent tuân theo các quy tắc **Outbound** của Security Group mà bạn liên kết với các ENI của Resource Gateway, và quy tắc **Inbound** của dịch vụ đích.
> 4.  **Service-linked Role với quyền hạn tối thiểu**: AWS DevOps Agent sử dụng một service-linked role bị giới hạn chặt chẽ trong các tài nguyên được gắn thẻ `AWSAIDevOpsManaged`. Nó **không thể truy cập bất kỳ tài nguyên nào khác** trong tài khoản của bạn.
> 5.  **Hỗ trợ DNS**: Bạn có thể tham chiếu các dịch vụ bằng tên DNS. Lưu ý: các tên DNS cần **phân giải được công khai** (publicly resolvable).
