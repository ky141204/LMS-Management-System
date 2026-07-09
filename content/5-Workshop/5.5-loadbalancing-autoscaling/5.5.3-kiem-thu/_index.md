---
title: "Test Auto Scaling"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 5.5.3. </b> "
---

<div class="lms">

# Confirm SNS and test Auto Scaling

Confirm the email subscription and generate simulated load to test automatic scaling.

**Open the email and click "Confirm subscription" to confirm the SNS subscription.**
![SNS subscription confirmation email](images/Screenshot%202026-07-09%20232607.png)

**The subscription is confirmed successfully.**
![SNS subscription confirmed successfully](images/Screenshot%202026-07-09%20232617.png)

**The Auto Scaling group is "At desired capacity"; review the activity history.**
![ASG status and activity](images/Screenshot%202026-07-09%20232717.png)

**Receive an email notification when an instance is launched (EC2_INSTANCE_LAUNCH).**
![Instance launch notification email](images/Screenshot%202026-07-09%20232751.png)

**Receive an email notification when an instance is terminated (EC2_INSTANCE_TERMINATE).**
![Instance termination notification email](images/Screenshot%202026-07-09%20232817.png)

**SSH into EC2 and install `stress-ng` to generate CPU load.**
![Install stress-ng](images/Screenshot%202026-07-09%20232859.png)

**Run `stress-ng --cpu 4 --timeout 600s` to increase CPU usage and trigger scaling/health events.**
![Run stress-ng to generate CPU load](images/Screenshot%202026-07-09%20232911.png)

</div>
