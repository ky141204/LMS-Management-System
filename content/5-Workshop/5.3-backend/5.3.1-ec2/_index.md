---
title: "Launch the EC2 Server"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

<div class="lms">

# Launch the backend EC2 server

Create an EC2 instance to run the LMS Node.js backend.

**Open the EC2 service, then choose Launch an instance.**
![Navigate to the EC2 service](images/Screenshot%202026-07-09%20225726.png)

**Name the instance `LMS-BACKEND-EC2`, choose the Amazon Linux 2023 AMI, and select the `t3.micro` instance type.**
![Set the name, AMI, and instance type](images/Screenshot%202026-07-09%20225738.png)

**Review the Amazon Linux 2023 AMI details (64-bit x86).**
![Amazon Linux 2023 AMI details](images/Screenshot%202026-07-09%20225743.png)

**Choose the `Khanh` key pair, place the instance in `LMS-VPC`, select a public subnet, and enable public IP assignment.**
![Choose the key pair and network settings](images/Screenshot%202026-07-09%20225800.png)

**Attach the existing `EC2-SG` security group and configure 8 GiB gp3 storage.**
![Choose EC2-SG and configure storage](images/Screenshot%202026-07-09%20225809.png)

**The instance launches successfully with the Running status and a public IP address.**
![LMS-BACKEND-EC2 is running](images/Screenshot%202026-07-09%20225827.png)

</div>
