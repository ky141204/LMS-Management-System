---
title: "Auto Scaling Group"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

<div class="lms">

# Create an Auto Scaling Group

Automatically increase or decrease the number of EC2 instances based on load so the system remains available.

**Create Auto Scaling group `LMS-ASG-TLP` and choose launch template `LMS-TPL`.**
![Create Auto Scaling group and choose launch template](images/Screenshot%202026-07-09%20232313.png)

**Review launch template details (AMI, t3.micro, key pair, security group).**
![Launch template details](images/Screenshot%202026-07-09%20232319.png)

**Choose VPC `LMS-VPC`.**
![Choose VPC for ASG](images/Screenshot%202026-07-09%20232345.png)

**Choose 2 public subnets and use "Balanced best effort" distribution.**
![Choose subnets for ASG](images/Screenshot%202026-07-09%20232351.png)

**Attach the ASG to the existing ALB by choosing target group `backend-tg`.**
![Attach ASG to the ALB target group](images/Screenshot%202026-07-09%20232400.png)

**Enable ELB health checks.**
![Configure health check (1)](images/Screenshot%202026-07-09%20232411.png)

**Set the health check grace period to 300 seconds.**
![Configure health check (2)](images/Screenshot%202026-07-09%20232415.png)

**Configure capacity: Desired 2, Min 2, Max 4.**
![Configure instance capacity](images/Screenshot%202026-07-09%20232429.png)

**Choose "No scaling policies" or add a policy based on your needs.**
![Configure scaling policy](images/Screenshot%202026-07-09%20232433.png)

**Enable group metrics collection for CloudWatch.**
![Enable CloudWatch group metrics](images/Screenshot%202026-07-09%20232441.png)

**Add SNS notifications to the administrator email for Launch/Terminate and other events.**
![Configure SNS notifications](images/Screenshot%202026-07-09%20232459.png)

**Skip tags, or add them if needed.**
![Add tags step](images/Screenshot%202026-07-09%20232513.png)

**Review everything and create the Auto Scaling group.**
![Review and create ASG](images/Screenshot%202026-07-09%20232522.png)

</div>
