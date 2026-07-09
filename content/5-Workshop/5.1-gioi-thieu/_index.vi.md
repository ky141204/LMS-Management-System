---
title: "Giới thiệu"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

<div class="lms">

# Giới thiệu

Workshop xây dựng **LMS-Management-System** — một hệ thống quản lý học tập trực tuyến hoàn chỉnh trên AWS theo kiến trúc **có tính sẵn sàng cao (High Availability)**. Người dùng truy cập qua **CloudFlare** và giao diện web trên **AWS Amplify**; backend Node.js chạy trên **EC2** phía sau **Application Load Balancer** kết hợp **Auto Scaling Group** trải trên 2 vùng khả dụng; dữ liệu lưu ở **Amazon DocumentDB** (Multi-AZ); hệ thống được giám sát bằng **CloudWatch**, **CloudTrail** và cảnh báo qua **Amazon SNS**.

### 🧾 Thông tin dự án sử dụng trong workshop

| Hạng mục | Giá trị |
|---|---|
| Khu vực (Region) | US East (N. Virginia) — `us-east-1` |
| VPC | `LMS-VPC` — `10.0.0.0/16` (2 AZ, 2 public + 2 private subnet) |
| Backend | Node.js chạy trên EC2, cổng `8080`, quản lý bằng PM2 |
| Mã nguồn | `github.com/huybee1403/LMS_System_MongoDB` |
| Cơ sở dữ liệu | Amazon DocumentDB 5.0 (`db.t3.medium`, Multi-AZ) |
| Tên miền | `fixing404.win` (API: `api.fixing404.win`) |

{{% notice note %}}
**Yêu cầu chuẩn bị:** Tài khoản AWS, một tên miền quản lý bằng CloudFlare, key pair EC2 (ở đây là `Khanh.pem`), và mã nguồn LMS trên GitHub (frontend + backend dạng monorepo).
{{% /notice %}}

![Kiến trúc tổng thể hệ thống LMS trên AWS](images/1.png)

</div>
