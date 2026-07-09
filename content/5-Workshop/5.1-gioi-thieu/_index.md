---
title: "Introduction"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

<div class="lms">

# Introduction

This workshop builds **LMS-Management-System**, a complete online learning management system on AWS using a **high availability** architecture. Users access the application through **CloudFlare** and a web frontend on **AWS Amplify**. The Node.js backend runs on **EC2** behind an **Application Load Balancer** with an **Auto Scaling Group** across 2 Availability Zones. Data is stored in **Amazon DocumentDB** (Multi-AZ), and the system is monitored with **CloudWatch**, **CloudTrail**, and alerts through **Amazon SNS**.

### Project information used in this workshop

| Item | Value |
|---|---|
| Region | US East (N. Virginia) - `us-east-1` |
| VPC | `LMS-VPC` - `10.0.0.0/16` (2 AZs, 2 public + 2 private subnets) |
| Backend | Node.js on EC2, port `8080`, managed with PM2 |
| Source code | `github.com/huybee1403/LMS_System_MongoDB` |
| Database | Amazon DocumentDB 5.0 (`db.t3.medium`, Multi-AZ) |
| Domain | `fixing404.win` (API: `api.fixing404.win`) |

{{% notice note %}}
**Prerequisites:** An AWS account, a domain managed in CloudFlare, an EC2 key pair (in this workshop, `Khanh.pem`), and the LMS source code on GitHub (frontend + backend in a monorepo).
{{% /notice %}}

![Overall LMS system architecture on AWS](images/1.png)

</div>
