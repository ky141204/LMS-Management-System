---
title: "Tạo VPC"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.2.1. </b> "
---

<div class="lms">

# Tạo VPC và hạ tầng mạng

Tạo mạng riêng ảo làm nền tảng cho toàn bộ hệ thống, gồm 2 vùng khả dụng để đảm bảo tính sẵn sàng cao.

**Mở dịch vụ VPC → nhấn Create VPC.**
![Trang tổng quan dịch vụ VPC](images/Screenshot%202026-07-09%20225444.png)

**Chọn "VPC and more", đặt tên `LMS-VPC`, dải địa chỉ IPv4 CIDR `10.0.0.0/16`.**
![Cấu hình tên và CIDR cho VPC](images/Screenshot%202026-07-09%20225512.png)

**Chọn 2 Availability Zone, 2 public subnet và 2 private subnet, NAT gateway = None.**
![Cấu hình số vùng khả dụng và subnet](images/Screenshot%202026-07-09%20225520.png)

**Bật VPC endpoint cho S3 (Gateway) và bật DNS hostnames / DNS resolution, sau đó Create VPC.**
![Cấu hình VPC endpoint và DNS](images/Screenshot%202026-07-09%20225524.png)

**VPC được tạo thành công (trạng thái Available).**
![VPC LMS-VPC đã tạo xong](images/Screenshot%202026-07-09%20225533.png)

**Vào mục Subnets để chỉnh sửa subnet công khai.**
![Danh sách 4 subnet của VPC](images/Screenshot%202026-07-09%20225541.png)

**Bật "Enable auto-assign public IPv4 address" cho các public subnet (để EC2 nhận IP công khai).**
![Bật tự động gán IP công khai cho public subnet](images/Screenshot%202026-07-09%20225547.png)

</div>
