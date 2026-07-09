---
title: "Dọn dẹp tài nguyên"
date: 2026-07-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

<div class="lms">

# Dọn dẹp tài nguyên

Sau khi hoàn thành workshop, cần dọn dẹp các tài nguyên đã triển khai để tránh phát sinh chi phí không cần thiết.

{{% notice warning %}}
Chỉ xóa các tài nguyên thuộc workshop này. Nếu một tài nguyên đang được dùng cho hệ thống khác, không xóa tài nguyên đó.
{{% /notice %}}

## Thứ tự dọn dẹp

{{% notice warning %}}
Nên xóa tài nguyên theo thứ tự: **Amplify → ACM → DocumentDB → Auto Scaling Group → Application Load Balancer/Target Group → EC2 instance → VPC**. Với DocumentDB, nếu có bật **Deletion protection**, cần tắt bảo vệ trước khi xóa cluster.
{{% /notice %}}

## 1. Xóa ứng dụng AWS Amplify

Vào **AWS Amplify**, mở ứng dụng frontend của workshop, kéo xuống phần **Delete app** trong **General settings**.

**Chọn `Delete app` để xóa ứng dụng Amplify đã triển khai.**
![Xóa ứng dụng Amplify](images/Screenshot%202026-07-09%20233448.png)

## 2. Xóa chứng chỉ ACM

Vào **AWS Certificate Manager**, chọn chứng chỉ SSL đã dùng cho domain của workshop. Nếu chứng chỉ không còn được dùng bởi tài nguyên nào khác, tiến hành xóa.

**Chọn chứng chỉ → More actions → Delete.**
![Xóa chứng chỉ ACM](images/Screenshot%202026-07-09%20233547.png)

## 3. Xóa Amazon DocumentDB

Vào **Amazon DocumentDB**, chọn cluster và instance đã tạo cho hệ thống LMS. Nếu cluster đang bật **Deletion protection**, hãy tắt bảo vệ trước rồi mới xóa.

**Chọn DocumentDB cluster hoặc instance → Actions → Delete.**
![Xóa DocumentDB cluster](images/Screenshot%202026-07-09%20233627.png)

## 4. Xóa Auto Scaling Group

Vào **EC2 → Auto Scaling Groups**, chọn Auto Scaling Group của workshop. Xóa ASG trước để AWS không tự tạo lại EC2 instance sau khi terminate.

**Chọn Auto Scaling Group → Actions → Delete.**
![Xóa Auto Scaling Group](images/Screenshot%202026-07-09%20233709.png)

## 5. Xóa Application Load Balancer

Vào **EC2 → Load Balancers**, chọn Application Load Balancer của backend. Sau khi xóa Load Balancer, tiếp tục xóa Target Group nếu Target Group không còn được sử dụng.

**Chọn Load Balancer → Actions → Delete load balancer.**
![Xóa Application Load Balancer](images/Screenshot%202026-07-09%20233727.png)

## 6. Terminate EC2 instance

Sau khi Auto Scaling Group đã được xóa, vào **EC2 → Instances** để terminate các instance còn lại thuộc workshop.

**Chọn các EC2 instance của hệ thống → Instance state → Terminate instance.**
![Chọn terminate các instance](images/Screenshot%202026-07-09%20233854.png)

**Xác nhận terminate để xóa các instance đang chạy.**
![Xác nhận terminate instance](images/Screenshot%202026-07-09%20233859.png)

## 7. Xóa VPC và tài nguyên mạng

Sau khi các tài nguyên phụ thuộc đã được xóa, vào **VPC console** để xóa VPC của workshop.

**Vào VPC → chọn VPC của workshop → Actions → Delete VPC.**
![Chọn xóa VPC](images/Screenshot%202026-07-09%20234028.png)

**Nhập `delete` để xác nhận xóa VPC cùng các tài nguyên mạng phụ thuộc còn lại.**
![Xác nhận xóa VPC](images/Screenshot%202026-07-09%20234544.png)

## 8. Xác nhận sau khi dọn dẹp

Sau khi xóa xong, kiểm tra lại các dịch vụ chính:

* AWS Amplify app đã được xóa.
* ACM certificate của workshop đã được xóa nếu không còn sử dụng.
* DocumentDB cluster và instance đã được xóa.
* Auto Scaling Group không còn tồn tại.
* Load Balancer và Target Group đã được xóa.
* EC2 instance không còn ở trạng thái `running`.
* VPC của workshop đã được xóa thành công.

## Kết luận

Sau khi dọn dẹp, hệ thống **LMS-Management-System** đã hoàn tất toàn bộ vòng đời triển khai trên AWS: xây dựng hạ tầng, triển khai backend/frontend, cấu hình cân bằng tải và Auto Scaling, giám sát hệ thống, sau đó xóa tài nguyên để kiểm soát chi phí. Đây là bước cuối quan trọng khi thực hành cloud, giúp đảm bảo môi trường lab không để lại tài nguyên phát sinh chi phí ngoài ý muốn.

</div>
