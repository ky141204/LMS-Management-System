---
title: "Create a DocumentDB Cluster (Multi-AZ)"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

<div class="lms">

# Create an Amazon DocumentDB cluster (Multi-AZ)

Create a document database that is compatible with MongoDB and placed in private subnets.

**Search for and open Amazon DocumentDB.**
![Navigate to Amazon DocumentDB](images/Screenshot%202026-07-09%20225845.png)

**Create a subnet group named `lms-docdb-subnet-group` in `LMS-VPC`.**
![Create a subnet group for DocumentDB](images/Screenshot%202026-07-09%20225927.png)

**Add 2 private subnets (us-east-1a and us-east-1b) to the subnet group.**
![Add private subnets to the subnet group](images/Screenshot%202026-07-09%20225932.png)

**The subnet group is created successfully with the Complete status.**
![Subnet group complete](images/Screenshot%202026-07-09%20225936.png)

**Create a cluster: choose Instance-based and engine version 5.0.0.**
![Create the DocumentDB cluster](images/Screenshot%202026-07-09%20225950.png)

**Choose the `db.t3.medium` instance class and enable 1 replica for Multi-AZ.**
![Choose instance class and replica](images/Screenshot%202026-07-09%20230001.png)

**Set the administrator credentials with username `admin404` and a password.**
![Configure login credentials](images/Screenshot%202026-07-09%20230020.png)

**Configure networking: VPC `LMS-VPC`, subnet group `lms-docdb-subnet-group`, and security group `DocumentDB-SG`.**
![Configure networking for the cluster](images/Screenshot%202026-07-09%20230038.png)

**Keep port `27017` and enable encryption at rest with the default KMS key.**
![Configure port and encryption](images/Screenshot%202026-07-09%20230044.png)

**Enable Deletion protection, review the estimated cost, then create the cluster.**
![Review and create the cluster](images/Screenshot%202026-07-09%20230052.png)

**The cluster reaches the Available status. Copy the connection string (endpoint) for the application.**
![DocumentDB cluster ready and connection string](images/Screenshot%202026-07-09%20230123.png)

</div>
