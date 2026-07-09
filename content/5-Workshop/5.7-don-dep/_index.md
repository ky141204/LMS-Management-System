---
title: "Clean Up Resources"
date: 2026-07-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

<div class="lms">

# Clean Up Resources

After completing the workshop, clean up the deployed resources to avoid unnecessary costs.

{{% notice warning %}}
Only delete resources that belong to this workshop. If a resource is being used by another system, do not delete it.
{{% /notice %}}

## Cleanup Order

{{% notice warning %}}
Delete resources in this order: **Amplify → ACM → DocumentDB → Auto Scaling Group → Application Load Balancer/Target Group → EC2 instance → VPC**. For DocumentDB, if **Deletion protection** is enabled, disable it before deleting the cluster.
{{% /notice %}}

## 1. Delete the AWS Amplify App

Go to **AWS Amplify**, open the frontend application for this workshop, and scroll down to **Delete app** in **General settings**.

**Choose `Delete app` to delete the deployed Amplify application.**
![Delete Amplify app](images/Screenshot%202026-07-09%20233448.png)

## 2. Delete the ACM Certificate

Go to **AWS Certificate Manager**, then select the SSL certificate used for the workshop domain. If the certificate is not used by any other resource, delete it.

**Select the certificate → More actions → Delete.**
![Delete ACM certificate](images/Screenshot%202026-07-09%20233547.png)

## 3. Delete Amazon DocumentDB

Go to **Amazon DocumentDB**, then select the cluster and instance created for the LMS system. If the cluster has **Deletion protection** enabled, disable it before deleting.

**Select the DocumentDB cluster or instance → Actions → Delete.**
![Delete DocumentDB cluster](images/Screenshot%202026-07-09%20233627.png)

## 4. Delete the Auto Scaling Group

Go to **EC2 → Auto Scaling Groups**, then select the Auto Scaling Group for this workshop. Delete the ASG first so AWS does not recreate EC2 instances after they are terminated.

**Select the Auto Scaling Group → Actions → Delete.**
![Delete Auto Scaling Group](images/Screenshot%202026-07-09%20233709.png)

## 5. Delete the Application Load Balancer

Go to **EC2 → Load Balancers**, then select the backend Application Load Balancer. After deleting the Load Balancer, delete the Target Group if it is no longer used.

**Select the Load Balancer → Actions → Delete load balancer.**
![Delete Application Load Balancer](images/Screenshot%202026-07-09%20233727.png)

## 6. Terminate EC2 Instances

After the Auto Scaling Group has been deleted, go to **EC2 → Instances** and terminate the remaining instances that belong to the workshop.

**Select the system EC2 instances → Instance state → Terminate instance.**
![Select instances to terminate](images/Screenshot%202026-07-09%20233854.png)

**Confirm termination to delete the running instances.**
![Confirm instance termination](images/Screenshot%202026-07-09%20233859.png)

## 7. Delete the VPC and Network Resources

After the dependent resources have been deleted, go to the **VPC console** and delete the workshop VPC.

**Go to VPC → select the workshop VPC → Actions → Delete VPC.**
![Choose delete VPC](images/Screenshot%202026-07-09%20234028.png)

**Enter `delete` to confirm deleting the VPC and its remaining dependent network resources.**
![Confirm VPC deletion](images/Screenshot%202026-07-09%20234544.png)

## 8. Confirm Cleanup

After deletion is complete, verify the main services:

* The AWS Amplify app has been deleted.
* The ACM certificate for the workshop has been deleted if it is no longer used.
* The DocumentDB cluster and instance have been deleted.
* The Auto Scaling Group no longer exists.
* The Load Balancer and Target Group have been deleted.
* No EC2 instance remains in the `running` state.
* The workshop VPC has been deleted successfully.

## Conclusion

After cleanup, **LMS-Management-System** has completed the full AWS deployment lifecycle: building infrastructure, deploying the backend and frontend, configuring load balancing and Auto Scaling, monitoring the system, and then deleting resources to control cost. This final step is important in cloud practice because it ensures the lab environment does not leave behind resources that continue to generate unexpected charges.

</div>
