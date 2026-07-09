---
title: "Create the VPC"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 5.2.1. </b> "
---

<div class="lms">

# Create the VPC and network infrastructure

Create a virtual private network as the foundation for the whole system, including 2 Availability Zones to support high availability.

**Open the VPC service, then choose Create VPC.**
![VPC service overview page](images/Screenshot%202026-07-09%20225444.png)

**Choose "VPC and more", set the name to `LMS-VPC`, and set the IPv4 CIDR block to `10.0.0.0/16`.**
![Configure the VPC name and CIDR](images/Screenshot%202026-07-09%20225512.png)

**Choose 2 Availability Zones, 2 public subnets, 2 private subnets, and NAT gateway = None.**
![Configure Availability Zones and subnets](images/Screenshot%202026-07-09%20225520.png)

**Enable the S3 Gateway VPC endpoint and enable DNS hostnames / DNS resolution, then create the VPC.**
![Configure the VPC endpoint and DNS](images/Screenshot%202026-07-09%20225524.png)

**The VPC is created successfully with the Available status.**
![LMS-VPC created successfully](images/Screenshot%202026-07-09%20225533.png)

**Go to Subnets to edit the public subnets.**
![List of 4 VPC subnets](images/Screenshot%202026-07-09%20225541.png)

**Enable "Enable auto-assign public IPv4 address" for the public subnets so EC2 instances can receive public IP addresses.**
![Enable auto-assign public IP for public subnets](images/Screenshot%202026-07-09%20225547.png)

</div>
