---
title: "Triển khai Frontend với Amplify"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

<div class="lms">

# Triển khai giao diện web với AWS Amplify

Deploy phần frontend (React/Vite) từ GitHub lên AWS Amplify.

**Mở dịch vụ AWS Amplify.**
![Điều hướng tới AWS Amplify](images/Screenshot%202026-07-09%20230957.png)

**Chọn nguồn mã là GitHub và cấp quyền truy cập.**
![Chọn nguồn mã GitHub](images/Screenshot%202026-07-09%20231022.png)

**Chọn repo `LMS_System_MongoDB`, nhánh `main`, đánh dấu monorepo với thư mục gốc `frontend`.**
![Chọn repo, nhánh và thư mục monorepo](images/Screenshot%202026-07-09%20231056.png)

**Cấu hình build: lệnh `npm run build`, thư mục output `dist`.**
![Cấu hình build của ứng dụng](images/Screenshot%202026-07-09%20231113.png)

**Thêm biến môi trường `VITE_BACKEND_URL = https://api.fixing404.win/api` để frontend gọi backend.**
![Thêm biến môi trường VITE_BACKEND_URL](images/Screenshot%202026-07-09%20231228.png)

**Xem lại cấu hình repo và nhánh.**
![Xem lại cấu hình (1)](images/Screenshot%202026-07-09%20231239.png)

**Xem lại cấu hình nâng cao và biến môi trường, rồi Save and deploy.**
![Xem lại cấu hình (2)](images/Screenshot%202026-07-09%20231245.png)

**Triển khai thành công — ứng dụng chạy tại tên miền `*.amplifyapp.com`.**
![Ứng dụng deploy thành công trên Amplify](images/Screenshot%202026-07-09%20231300.png)

</div>
