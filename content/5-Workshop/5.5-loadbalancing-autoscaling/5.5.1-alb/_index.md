---
title: "Target Group and Load Balancer"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

<div class="lms">

# Create a Target Group and Application Load Balancer

Create a load balancer to distribute traffic to the backend.

**Create an Instances target group named `backend-tg`.**
![Create the backend-tg target group](images/Screenshot%202026-07-09%20231910.png)

**Configure HTTP protocol, port `8080`, in VPC `LMS-VPC`.**
![Configure target group protocol and port](images/Screenshot%202026-07-09%20231930.png)

**Configure the health check with HTTP protocol and path `/`.**
![Configure health check](images/Screenshot%202026-07-09%20231940.png)

**Continue to the target registration step.**
![Continue to target registration](images/Screenshot%202026-07-09%20231945.png)

**Choose the `LMS-BACKEND-EC2` instance on port 8080.**
![Choose the instance to register](images/Screenshot%202026-07-09%20232017.png)

**The instance is added to the target list.**
![Instance added as a target](images/Screenshot%202026-07-09%20232026.png)

**Review and create the target group.**
![Review and create the target group](images/Screenshot%202026-07-09%20232036.png)

**The `backend-tg` target group is created with healthy status.**
![Target group created successfully](images/Screenshot%202026-07-09%20232113.png)

**Start creating a Load Balancer and choose Application Load Balancer.**
![Compare and choose the Load Balancer type](images/Screenshot%202026-07-09%20232130.png)

**Set the name to `LMS-BACKEND-ALB`, choose Internet-facing, and use IPv4.**
![Configure basic ALB settings](images/Screenshot%202026-07-09%20232144.png)

**Network mapping: choose 2 public subnets (us-east-1a and us-east-1b).**
![Configure network mapping for the ALB](images/Screenshot%202026-07-09%20232202.png)

**Attach security group `ALB-SG` and create an HTTP:80 listener.**
![Configure security group and listener](images/Screenshot%202026-07-09%20232214.png)

**Set the listener default action to forward to `backend-tg`.**
![Configure forwarding to the target group](images/Screenshot%202026-07-09%20232225.png)

**Review the full configuration (1).**
![Review ALB configuration (1)](images/Screenshot%202026-07-09%20232232.png)

**Review and choose Create load balancer (2).**
![Review ALB configuration (2)](images/Screenshot%202026-07-09%20232236.png)

**The `LMS-BACKEND-ALB` is Active.**
![ALB is active](images/Screenshot%202026-07-09%20232242.png)

</div>
