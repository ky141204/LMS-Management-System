---
title: "Blog 3"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Giám sát chủ động cho Amazon Redshift Serverless bằng AWS Lambda và cảnh báo Slack
---

> [!IMPORTANT]
> ### 🎯 Mục tiêu bài viết
> Bài viết này hướng dẫn cách **xây dựng hệ thống giám sát chủ động (proactive monitoring)** cho **Amazon Redshift Serverless**, giúp phát hiện sớm các vấn đề hiệu suất như truy vấn chậm, hàng đợi tăng cao hoặc biến động tài nguyên — đồng thời gửi cảnh báo thời gian thực đến Slack để đội ngũ phản ứng nhanh chóng mà không cần theo dõi dashboard liên tục.
>
> *   **Bài viết gốc đăng tải tại:** [AWS Study Group](https://awsstudygroup.com/2026/05/14/giam-sat-chu-dong-cho-amazon-redshift-serverless-bang-aws-lambda-va-canh-bao-slack/)

---

## 1. Giới thiệu về Amazon Redshift Serverless

**Amazon Redshift Serverless** Trong các hệ thống phân tích dữ liệu hiện đại, các vấn đề về hiệu suất thường không được phát hiện sớm mà chỉ xuất hiện khi đã gây ảnh hưởng trực tiếp đến hệ thống, chẳng hạn như:

* Dashboard bị chậm hoặc gián đoạn
* Pipeline ETL bị delay
* Quyết định kinh doanh bị ảnh hưởng do dữ liệu không kịp thời

**Đối với Amazon Redshift Serverless**, mặc dù đã loại bỏ nhu cầu quản lý hạ tầng, nhưng vẫn tồn tại các rủi ro:

* Truy vấn chạy lâu bất thường
* Hàng đợi truy vấn tăng cao
* Tăng đột biến tài nguyên tính toán (RPU)

Những vấn đề này nếu không được phát hiện kịp thời sẽ dẫn đến giảm hiệu suất hệ thống và tăng chi phí vận hành.
---

## 2. Giải pháp: Giám sát chủ động (Proactive Monitoring)

Giải pháp đề xuất sử dụng kiến trúc serverless hoàn toàn để tự động theo dõi và cảnh báo hiệu suất của **Amazon Redshift Serverless.**

Hệ thống giúp:

* Phát hiện sớm các vấn đề hiệu suất trước khi ảnh hưởng người dùng
* Giảm thiểu downtime và độ trễ của hệ thống phân tích
* Kiểm soát chi phí thông qua theo dõi RPU usage

Giải pháp có thể áp dụng cho nhiều trường hợp:

Dashboard BI (Power BI, Tableau…)
Pipeline ETL/ELT
Hệ thống phân tích dữ liệu real-time

### Cơ chế hoạt động

Hệ thống sử dụng các dịch vụ AWS để thu thập, phân tích và gửi cảnh báo:

* Amazon EventBridge – kích hoạt theo lịch
* AWS Lambda – xử lý và đánh giá dữ liệu
* Amazon CloudWatch – cung cấp metrics
* Amazon SNS – gửi cảnh báo
* Amazon Q Developer in Chat applications – tích hợp Slack

🔄 Quy trình hoạt động

1. Trigger theo lịch
Amazon EventBridge kích hoạt AWS Lambda định kỳ (ví dụ: 15 phút/lần).

2. Thu thập chỉ số
Lambda lấy dữ liệu từ:

* Amazon CloudWatch
* Redshift Data API

Bao gồm:

* Query đang chờ / đang chạy
* Truy vấn chậm
* RPUs (compute usage)
* Storage usage
* Số lượng kết nối
3. Đánh giá ngưỡng
So sánh metrics với các threshold cấu hình trước.
4. Gửi cảnh báo
Nếu vượt ngưỡng → gửi message đến Amazon SNS.
5. Thông báo Slack
Amazon Q Developer in Chat applications gửi cảnh báo đến kênh Slack.

## 3. Kiến trúc tổng thể

![Kiến trúc Giám sát chủ động cho Amazon Redshift Serverless bằng AWS Lambda và cảnh báo Slack](images/Screenshot_2026-07-03_161351.png)

### Luồng hoạt động (End-to-End Flow)

| Bước | Thành phần | Mô tả |
| :---: | :--- | :--- |
| **①** | **EventBridge → Lambda** | Kích hoạt thu thập dữ liệu theo lịch. |
| **②** | **Lambda → CloudWatch / Redshift** | Lấy metrics & query data. |
| **③** | **Lambda (Evaluation)** | So sánh với threshold. |
| **④** | **Lambda → SNS** | Gửi cảnh báo khi bất thường. |
| **⑤** | **SNS → Slack** | Thông báo real-time qua Chatbot. |
| **⑥** | **CloudWatch Logs** | Lưu log để debug & audit. |

⚙️ Mô tả kiến trúc
* Amazon EventBridge đảm nhiệm việc trigger tự động
* AWS Lambda là trung tâm xử lý logic
* Amazon CloudWatch cung cấp dữ liệu quan sát
* Amazon SNS đảm nhiệm gửi alert
* Slack integration giúp hiển thị cảnh báo trực tiếp cho team

---

## 4. Các lớp bảo mật

> [!TIP]
> ### 🔐 Bảo mật & vận hành hiệu quả
>
> Giải pháp đảm bảo an toàn và dễ vận hành:
>
> 1.  **Serverless hoàn toàn**: Không cần quản lý server → giảm rủi ro cấu hình sai.
> 2.  **IAM Role phân quyền tối thiểu**: Lambda chỉ truy cập đúng tài nguyên cần thiết.
> 3.  **CloudWatch Logs để audit**: Tất cả hoạt động được ghi lại phục vụ debug.
> 4.  **Không cần public endpoint**: Toàn bộ giao tiếp nằm trong AWS services.
> 5.  **Dễ mở rộng**: Có thể thêm nhiều rule, nhiều workspace Redshift.
