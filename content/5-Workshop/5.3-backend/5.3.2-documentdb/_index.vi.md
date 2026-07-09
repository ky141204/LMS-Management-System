---
title: "Tạo cụm DocumentDB (Multi-AZ)"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

<div class="lms">

# Tạo cụm Amazon DocumentDB (Multi-AZ)

Tạo cơ sở dữ liệu tài liệu (tương thích MongoDB) đặt trong private subnet.

**Tìm và mở dịch vụ Amazon DocumentDB.**
![Điều hướng tới Amazon DocumentDB](images/Screenshot%202026-07-09%20225845.png)

**Tạo Subnet group `lms-docdb-subnet-group` trong VPC `LMS-VPC`.**
![Tạo subnet group cho DocumentDB](images/Screenshot%202026-07-09%20225927.png)

**Thêm 2 private subnet (us-east-1a và us-east-1b) vào subnet group.**
![Thêm private subnet vào subnet group](images/Screenshot%202026-07-09%20225932.png)

**Subnet group tạo xong (trạng thái Complete).**
![Subnet group hoàn tất](images/Screenshot%202026-07-09%20225936.png)

**Tạo cluster: loại Instance-based, engine version 5.0.0.**
![Tạo cluster DocumentDB](images/Screenshot%202026-07-09%20225950.png)

**Chọn instance class `db.t3.medium` và bật 1 bản sao (replica) để có Multi-AZ.**
![Chọn instance class và replica](images/Screenshot%202026-07-09%20230001.png)

**Đặt tài khoản quản trị (username `admin404`) và mật khẩu.**
![Cấu hình tài khoản đăng nhập](images/Screenshot%202026-07-09%20230020.png)

**Cấu hình mạng: VPC `LMS-VPC`, subnet group `lms-docdb-subnet-group`, security group `DocumentDB-SG`.**
![Cấu hình mạng cho cluster](images/Screenshot%202026-07-09%20230038.png)

**Giữ cổng `27017`, bật mã hóa khi lưu trữ (encryption at rest) bằng khóa KMS mặc định.**
![Cấu hình cổng và mã hóa](images/Screenshot%202026-07-09%20230044.png)

**Bật Deletion protection, xem lại ước tính chi phí rồi Create cluster.**
![Xem lại và tạo cluster](images/Screenshot%202026-07-09%20230052.png)

**Cluster ở trạng thái Available, lấy chuỗi kết nối (endpoint) để ứng dụng dùng.**
![Cluster DocumentDB sẵn sàng và chuỗi kết nối](images/Screenshot%202026-07-09%20230123.png)

</div>
