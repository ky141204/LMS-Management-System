---
title: "Blog 3"
date: 2026-07-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Proactive Monitoring for Amazon Redshift Serverless with AWS Lambda and Slack Alerts
---

> [!IMPORTANT]
> ### 🎯 Article goal
> This article explains how to **build a proactive monitoring system** for **Amazon Redshift Serverless**, helping detect performance issues early, such as slow queries, increasing queues, or resource fluctuations, while sending real-time alerts to Slack so teams can respond quickly without continuously watching dashboards.
>
> * **Original article published at:** [AWS Study Group](https://awsstudygroup.com/2026/05/14/giam-sat-chu-dong-cho-amazon-redshift-serverless-bang-aws-lambda-va-canh-bao-slack/)

---

## 1. Introduction to Amazon Redshift Serverless

**Amazon Redshift Serverless** In modern data analytics systems, performance problems are often not detected early and only appear after they have directly affected the system, such as:

* Slow or interrupted dashboards
* Delayed ETL pipelines
* Business decisions affected because data is not timely

**For Amazon Redshift Serverless**, although it removes the need to manage infrastructure, there are still risks:

* Queries running unusually long
* Query queues increasing
* Sudden spikes in compute resources (RPU)

If these issues are not detected in time, they can reduce system performance and increase operating costs.

---

## 2. Solution: Proactive Monitoring

The proposed solution uses a fully serverless architecture to automatically monitor and alert on the performance of **Amazon Redshift Serverless**.

The system helps:

* Detect performance issues before they affect users
* Reduce downtime and latency in analytics systems
* Control cost by tracking RPU usage

The solution can be applied to many use cases:

* BI dashboards (Power BI, Tableau, ...)
* ETL/ELT pipelines
* Real-time data analytics systems

### How it works

The system uses AWS services to collect, analyze, and send alerts:

* Amazon EventBridge - scheduled trigger
* AWS Lambda - data processing and evaluation
* Amazon CloudWatch - metrics provider
* Amazon SNS - alert delivery
* Amazon Q Developer in Chat applications - Slack integration

🔄 Operating workflow

1. Scheduled trigger

Amazon EventBridge triggers AWS Lambda periodically, for example every 15 minutes.

2. Metric collection

Lambda retrieves data from:

* Amazon CloudWatch
* Redshift Data API

Including:

* Waiting/running queries
* Slow queries
* RPUs (compute usage)
* Storage usage
* Number of connections

3. Threshold evaluation

Compare metrics against preconfigured thresholds.

4. Send alert

If a threshold is exceeded → send a message to Amazon SNS.

5. Slack notification

Amazon Q Developer in Chat applications sends the alert to a Slack channel.

## 3. Overall architecture

![Proactive monitoring architecture for Amazon Redshift Serverless with AWS Lambda and Slack alerts](images/Screenshot_2026-07-03_161351.png)

### End-to-End Flow

| Step | Component | Description |
| :---: | :--- | :--- |
| **①** | **EventBridge → Lambda** | Triggers scheduled data collection. |
| **②** | **Lambda → CloudWatch / Redshift** | Retrieves metrics and query data. |
| **③** | **Lambda (Evaluation)** | Compares data with thresholds. |
| **④** | **Lambda → SNS** | Sends alerts when abnormalities occur. |
| **⑤** | **SNS → Slack** | Sends real-time notifications through Chatbot. |
| **⑥** | **CloudWatch Logs** | Stores logs for debugging and auditing. |

⚙️ Architecture description

* Amazon EventBridge handles automatic triggering
* AWS Lambda is the logic processing center
* Amazon CloudWatch provides observability data
* Amazon SNS handles alert delivery
* Slack integration displays alerts directly to the team

---

## 4. Security layers

> [!TIP]
> ### 🔐 Security and effective operations
>
> The solution is secure and easy to operate:
>
> 1. **Fully serverless**: No server management is required, reducing misconfiguration risk.
> 2. **Least-privilege IAM Role**: Lambda only accesses the resources it needs.
> 3. **CloudWatch Logs for audit**: All activities are logged for debugging.
> 4. **No public endpoint required**: All communication stays within AWS services.
> 5. **Easy to scale**: More rules and more Redshift workspaces can be added.
