---
title: "Khởi tạo máy chủ EC2"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

<div class="lms">

# Khởi tạo máy chủ EC2 backend

Tạo một EC2 chạy backend Node.js của hệ thống LMS.

**Mở dịch vụ EC2 → Launch an instance.**
![Điều hướng tới dịch vụ EC2](images/Screenshot%202026-07-09%20225726.png)

**Đặt tên `LMS-BACKEND-EC2`, chọn AMI Amazon Linux 2023, loại `t3.micro`.**
![Đặt tên và chọn AMI, instance type](images/Screenshot%202026-07-09%20225738.png)

**Xem chi tiết AMI Amazon Linux 2023 (64-bit x86).**
![Chi tiết AMI Amazon Linux 2023](images/Screenshot%202026-07-09%20225743.png)

**Chọn key pair `Khanh`, đặt máy trong VPC `LMS-VPC`, public subnet, bật gán IP công khai.**
![Chọn key pair và cấu hình mạng](images/Screenshot%202026-07-09%20225800.png)

**Gắn security group có sẵn `EC2-SG` và cấu hình ổ đĩa 8 GiB gp3.**
![Chọn EC2-SG và cấu hình lưu trữ](images/Screenshot%202026-07-09%20225809.png)

**Instance khởi chạy thành công (Running) và có IP công khai.**
![EC2 LMS-BACKEND-EC2 đang chạy](images/Screenshot%202026-07-09%20225827.png)

</div>
