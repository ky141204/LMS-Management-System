---
title: "Auto Scaling Group"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

<div class="lms">

# Tạo Auto Scaling Group

Tự động tăng/giảm số lượng EC2 theo tải, đảm bảo hệ thống luôn sẵn sàng.

**Tạo Auto Scaling group `LMS-ASG-TLP`, chọn launch template `LMS-TPL`.**
![Tạo Auto Scaling group và chọn launch template](images/Screenshot%202026-07-09%20232313.png)

**Xem lại thông tin launch template (AMI, t3.micro, key pair, security group).**
![Chi tiết launch template](images/Screenshot%202026-07-09%20232319.png)

**Chọn VPC `LMS-VPC`.**
![Chọn VPC cho ASG](images/Screenshot%202026-07-09%20232345.png)

**Chọn 2 public subnet, phân bổ "Balanced best effort".**
![Chọn subnet cho ASG](images/Screenshot%202026-07-09%20232351.png)

**Gắn ASG vào ALB có sẵn — chọn target group `backend-tg`.**
![Gắn ASG vào target group của ALB](images/Screenshot%202026-07-09%20232400.png)

**Bật health check của ELB.**
![Cấu hình health check (1)](images/Screenshot%202026-07-09%20232411.png)

**Đặt thời gian chờ khởi động (grace period) 300 giây.**
![Cấu hình health check (2)](images/Screenshot%202026-07-09%20232415.png)

**Cấu hình dung lượng: Desired 2, Min 2, Max 4.**
![Cấu hình số lượng instance](images/Screenshot%202026-07-09%20232429.png)

**Chọn "No scaling policies" (hoặc thêm chính sách tùy nhu cầu).**
![Cấu hình chính sách mở rộng](images/Screenshot%202026-07-09%20232433.png)

**Bật thu thập số liệu nhóm (CloudWatch group metrics).**
![Bật thu thập metrics cho CloudWatch](images/Screenshot%202026-07-09%20232441.png)

**Thêm thông báo qua SNS tới email quản trị (mọi sự kiện Launch/Terminate...).**
![Cấu hình thông báo SNS](images/Screenshot%202026-07-09%20232459.png)

**Bỏ qua tags (tùy chọn).**
![Bước thêm tags](images/Screenshot%202026-07-09%20232513.png)

**Xem lại toàn bộ và tạo Auto Scaling group.**
![Xem lại và tạo ASG](images/Screenshot%202026-07-09%20232522.png)

</div>
