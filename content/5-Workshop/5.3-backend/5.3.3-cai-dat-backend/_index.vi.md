---
title: "Cài đặt & chạy Backend"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 5.3.3. </b> "
---

<div class="lms">

# Cài đặt và chạy backend trên EC2

Kết nối SSH vào EC2, cài môi trường và chạy ứng dụng backend.

**Mở Terminal/PowerShell tại thư mục chứa key.**
![Mở terminal](images/Screenshot%202026-07-09%20230133.png)

**SSH vào EC2 bằng lệnh `ssh -i "Khanh.pem" ec2-user@<public-dns>`.**
![Kết nối SSH vào EC2](images/Screenshot%202026-07-09%20230210.png)

**Cập nhật hệ thống và cài `git` (`sudo dnf update -y`, `sudo dnf install git -y`).**
![Cập nhật hệ thống và cài git](images/Screenshot%202026-07-09%20230221.png)

**Quá trình cài git hoàn tất.**
![Cài git hoàn tất](images/Screenshot%202026-07-09%20230254.png)

**Cài Node.js (`sudo dnf install nodejs -y`).**
![Cài Node.js](images/Screenshot%202026-07-09%20230304.png)

**Clone mã nguồn LMS, vào thư mục `backend` và chạy `npm install`.**
![Clone mã nguồn và cài dependencies](images/Screenshot%202026-07-09%20230320.png)

**Tải chứng chỉ CA của DocumentDB (`global-bundle.pem`), chạy thử `npm start` (kết nối DB thành công, cổng 8080), rồi cài PM2.**
![Tải CA cert, chạy thử và cài PM2](images/Screenshot%202026-07-09%20230354.png)

**Kiểm tra PM2 đã cài (`pm2 -v`).**
![Kiểm tra phiên bản PM2](images/Screenshot%202026-07-09%20230401.png)

**Chạy backend nền bằng `pm2 start server.js --name backend`, rồi `pm2 save` để tự khởi động lại.**
![Chạy backend bằng PM2 và lưu cấu hình](images/Screenshot%202026-07-09%20230533.png)

</div>
