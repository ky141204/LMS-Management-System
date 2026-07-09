---
title: "Create Security Groups"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 5.2.2. </b> "
---

<div class="lms">

# Create Security Groups

Create 3 security groups for the 3 layers: load balancer, application server, and database.

**`ALB-SG`: allow HTTP (80) and HTTPS (443) from the Internet.**
![ALB-SG security group](images/Screenshot%202026-07-09%20225627.png)

**`DocumentDB-SG`: allow port `27017` (DocumentDB/MongoDB port) for the data layer.**
![DocumentDB-SG security group](images/Screenshot%202026-07-09%20225635.png)

**`EC2-SG`: allow the required ports: SSH (22), HTTP (80), HTTPS (443), and the application port (8080).**
![EC2-SG security group](images/Screenshot%202026-07-09%20225643.png)

</div>
