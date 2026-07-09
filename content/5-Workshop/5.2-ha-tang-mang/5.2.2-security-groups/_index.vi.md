---
title: "Tạo Security Groups"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 5.2.2. </b> "
---

<div class="lms">

# Tạo các Security Group

Tạo 3 nhóm bảo mật tương ứng 3 lớp: cân bằng tải, máy chủ ứng dụng và cơ sở dữ liệu.

**`ALB-SG`: mở cổng HTTP (80) và HTTPS (443) từ Internet.**
![Security group ALB-SG](images/Screenshot%202026-07-09%20225627.png)

**`DocumentDB-SG`: mở cổng `27017` (cổng của DocumentDB/MongoDB) cho lớp dữ liệu.**
![Security group DocumentDB-SG](images/Screenshot%202026-07-09%20225635.png)

**`EC2-SG`: mở các cổng cần thiết — SSH (22), HTTP (80), HTTPS (443) và ứng dụng (8080).**
![Security group EC2-SG](images/Screenshot%202026-07-09%20225643.png)

</div>
