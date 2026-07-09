---
title: "Giám sát hệ thống"
date: 2026-07-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

<div class="lms">

# Giám sát hệ thống

Theo dõi hiệu năng và nhật ký hoạt động của hệ thống bằng **CloudWatch** và **CloudTrail**.

## Giám sát với CloudWatch & CloudTrail

**Xem danh sách EC2 (các instance do ASG quản lý).**
![Danh sách EC2 instance](images/Screenshot%202026-07-09%20232926.png)

**Tab Monitoring của instance — biểu đồ CPU, mạng, credit.**
![Giám sát instance với CloudWatch](images/Screenshot%202026-07-09%20232956.png)

**Mở dịch vụ CloudWatch.**
![Điều hướng tới CloudWatch](images/Screenshot%202026-07-09%20233028.png)

**Xem chỉ số của Application Load Balancer.**
![Chỉ số CloudWatch của ALB](images/Screenshot%202026-07-09%20233139.png)

**Xem chỉ số của Auto Scaling Group.**
![Chỉ số CloudWatch của ASG](images/Screenshot%202026-07-09%20233156.png)

**Duyệt các namespace chỉ số khác trong CloudWatch.**
![Duyệt các chỉ số trong CloudWatch](images/Screenshot%202026-07-09%20233210.png)

**Xem chỉ số CPUUtilization của EC2 theo Auto Scaling Group.**
![Chỉ số CPU của EC2 theo ASG](images/Screenshot%202026-07-09%20233230.png)

**Mở dịch vụ CloudTrail để kiểm tra nhật ký hoạt động.**
![Điều hướng tới CloudTrail](images/Screenshot%202026-07-09%20233237.png)

**Xem lịch sử sự kiện ghi (write) — các thao tác của Auto Scaling.**
![Lịch sử sự kiện trong CloudTrail](images/Screenshot%202026-07-09%20233403.png)

**So sánh chi tiết các sự kiện (nguồn, IP, request ID).**
![So sánh chi tiết sự kiện CloudTrail](images/Screenshot%202026-07-09%20233412.png)

</div>
