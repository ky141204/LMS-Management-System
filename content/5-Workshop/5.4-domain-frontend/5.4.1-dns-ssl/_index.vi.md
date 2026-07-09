---
title: "DNS & chứng chỉ SSL"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

<div class="lms">

# Cấu hình DNS (CloudFlare) và chứng chỉ SSL (ACM)

Trỏ tên miền về ALB và cấp chứng chỉ HTTPS cho API.

**Trong CloudFlare, tạo bản ghi CNAME `api.fixing404.win` trỏ về DNS của ALB.**
![Tạo bản ghi CNAME trong CloudFlare](images/Screenshot%202026-07-09%20230654.png)

**Mở AWS Certificate Manager (ACM).**
![Điều hướng tới ACM](images/Screenshot%202026-07-09%20230713.png)

**Chọn "Request a public certificate".**
![Yêu cầu chứng chỉ công khai](images/Screenshot%202026-07-09%20230901.png)

**Nhập tên miền `api.fixing404.win`, chọn phương thức xác thực DNS.**
![Nhập domain và chọn xác thực DNS](images/Screenshot%202026-07-09%20230927.png)

**Chọn thuật toán khóa RSA 2048.**
![Chọn thuật toán khóa RSA 2048](images/Screenshot%202026-07-09%20230934.png)

**Gửi yêu cầu (Request).**
![Gửi yêu cầu chứng chỉ](images/Screenshot%202026-07-09%20230938.png)

**Sau khi thêm bản ghi CNAME xác thực vào CloudFlare, chứng chỉ chuyển sang trạng thái Issued.**
![Chứng chỉ đã được cấp (Issued)](images/Screenshot%202026-07-09%20230949.png)

</div>
