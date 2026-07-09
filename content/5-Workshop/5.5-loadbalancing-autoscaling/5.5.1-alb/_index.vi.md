---
title: "Target Group & Load Balancer"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

<div class="lms">

# Tạo Target Group và Application Load Balancer

Tạo bộ cân bằng tải phân phối lưu lượng tới backend.

**Tạo Target group loại Instances, đặt tên `backend-tg`.**
![Tạo target group backend-tg](images/Screenshot%202026-07-09%20231910.png)

**Cấu hình giao thức HTTP, cổng `8080`, trong VPC `LMS-VPC`.**
![Cấu hình giao thức và cổng cho target group](images/Screenshot%202026-07-09%20231930.png)

**Cấu hình health check giao thức HTTP, đường dẫn `/`.**
![Cấu hình health check](images/Screenshot%202026-07-09%20231940.png)

**Tiếp tục sang bước đăng ký target.**
![Chuyển sang đăng ký target](images/Screenshot%202026-07-09%20231945.png)

**Chọn instance `LMS-BACKEND-EC2`, cổng 8080.**
![Chọn instance để đăng ký](images/Screenshot%202026-07-09%20232017.png)

**Instance được thêm vào danh sách target.**
![Instance đã được thêm làm target](images/Screenshot%202026-07-09%20232026.png)

**Xem lại và tạo target group.**
![Xem lại và tạo target group](images/Screenshot%202026-07-09%20232036.png)

**Target group `backend-tg` đã tạo (trạng thái healthy).**
![Target group đã tạo xong](images/Screenshot%202026-07-09%20232113.png)

**Bắt đầu tạo Load Balancer — chọn loại Application Load Balancer.**
![So sánh và chọn loại Load Balancer](images/Screenshot%202026-07-09%20232130.png)

**Đặt tên `LMS-BACKEND-ALB`, kiểu Internet-facing, IPv4.**
![Cấu hình cơ bản của ALB](images/Screenshot%202026-07-09%20232144.png)

**Ánh xạ mạng: chọn 2 public subnet (us-east-1a và us-east-1b).**
![Cấu hình network mapping cho ALB](images/Screenshot%202026-07-09%20232202.png)

**Gắn security group `ALB-SG` và tạo listener HTTP:80.**
![Cấu hình security group và listener](images/Screenshot%202026-07-09%20232214.png)

**Đặt hành động mặc định của listener là forward tới `backend-tg`.**
![Cấu hình forward tới target group](images/Screenshot%202026-07-09%20232225.png)

**Xem lại toàn bộ cấu hình (1).**
![Xem lại cấu hình ALB (1)](images/Screenshot%202026-07-09%20232232.png)

**Xem lại và nhấn Create load balancer (2).**
![Xem lại cấu hình ALB (2)](images/Screenshot%202026-07-09%20232236.png)

**ALB `LMS-BACKEND-ALB` đã Active.**
![ALB đã hoạt động](images/Screenshot%202026-07-09%20232242.png)

</div>
