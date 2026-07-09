---
title: "Kiểm thử Auto Scaling"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 5.5.3. </b> "
---

<div class="lms">

# Xác nhận SNS và kiểm thử Auto Scaling

Xác nhận đăng ký email và tạo tải giả để kiểm tra khả năng tự mở rộng.

**Mở email và bấm "Confirm subscription" để xác nhận đăng ký SNS.**
![Email xác nhận đăng ký SNS](images/Screenshot%202026-07-09%20232607.png)

**Đăng ký được xác nhận thành công.**
![Xác nhận đăng ký SNS thành công](images/Screenshot%202026-07-09%20232617.png)

**Auto Scaling group ở trạng thái "At desired capacity", xem lịch sử hoạt động.**
![Trạng thái và hoạt động của ASG](images/Screenshot%202026-07-09%20232717.png)

**Nhận email thông báo khi có instance được khởi chạy (EC2_INSTANCE_LAUNCH).**
![Email thông báo instance khởi chạy](images/Screenshot%202026-07-09%20232751.png)

**Nhận email thông báo khi có instance bị thu hồi (EC2_INSTANCE_TERMINATE).**
![Email thông báo instance bị thu hồi](images/Screenshot%202026-07-09%20232817.png)

**SSH vào EC2, cài công cụ `stress-ng` để tạo tải CPU.**
![Cài đặt stress-ng](images/Screenshot%202026-07-09%20232859.png)

**Chạy `stress-ng --cpu 4 --timeout 600s` để đẩy CPU lên cao, kích hoạt sự kiện scaling/health.**
![Chạy stress-ng tạo tải CPU](images/Screenshot%202026-07-09%20232911.png)

</div>
