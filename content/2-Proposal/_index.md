---
title: "Proposal"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

## Deploying LMS-Management-System on AWS with AWS Amplify, Amazon EC2, Amazon DocumentDB, and a Distributed Architecture

### 1. Executive Summary

This proposal presents the deployment of **LMS-Management-System** on AWS using a distributed architecture. The system supports learning management features such as user management, courses, lessons, learning progress, assignments, and administration. Users access the system through a domain managed by Cloudflare. The frontend is deployed with AWS Amplify, while backend API traffic is routed through an Application Load Balancer to EC2 instances running inside an Auto Scaling Group.

The system uses Amazon DocumentDB as the primary database for document-based LMS data such as users, courses, lessons, submissions, and learning status. The database is placed in private subnets with Multi-AZ replication for higher availability. Monitoring is handled by Amazon CloudWatch, CloudWatch Alarm, Amazon SNS, and email notifications so administrators can react quickly when issues appear.

### 2. Problem Statement

#### What's the Problem?

Small LMS applications are often deployed on a single server, which creates several risks:

- The server can become overloaded when traffic increases.
- A single server or database failure can interrupt the whole application.
- Logs, metrics, and alerts are not always automated.
- HTTPS certificates, DNS, and security settings can be difficult to maintain manually.
- Learning data such as course progress, submissions, and activity history needs stable and scalable storage.

#### The Solution

The proposed solution uses a cloud-native AWS architecture that separates the frontend, backend, database, and monitoring layers. Cloudflare manages DNS and protects the first access layer. AWS Amplify hosts the frontend and uses an SSL/TLS certificate from AWS Certificate Manager. LMS backend services run on EC2 instances behind an Application Load Balancer, with an Auto Scaling Group to adjust capacity based on demand. Amazon DocumentDB is deployed in private subnets to prevent direct public access and to fit the document-oriented data model of the LMS.

#### Benefits and Return on Investment

- Higher availability through multiple Availability Zones.
- Automatic backend scaling with Auto Scaling Group.
- Better security by separating public and private subnets.
- Automated monitoring, alarms, and email notifications.
- A reusable foundation for LMS features such as courses, classes, lessons, learning progress, submissions, and user accounts.

### 3. Solution Architecture

The proposed architecture is shown below:

![AWS Web Application Architecture](images/1.png)

Main request flow:

1. The user sends an HTTPS request to the application domain.
2. Cloudflare resolves DNS and routes traffic toward AWS.
3. AWS Amplify serves the frontend and uses SSL/TLS from AWS Certificate Manager.
4. API requests are forwarded to the Application Load Balancer.
5. The ALB distributes requests to EC2 instances in public subnets.
6. EC2 instances read and write LMS data to Amazon DocumentDB in private subnets.
7. DocumentDB replication across two Availability Zones improves data availability.
8. EC2 instances send metrics and logs to Amazon CloudWatch.
9. CloudWatch Alarm triggers when the system exceeds defined thresholds.
10. Amazon SNS sends email notifications to administrators.

#### AWS Services Used

- **AWS Amplify**: Hosts and deploys the frontend application.
- **AWS Certificate Manager**: Manages SSL/TLS certificates for HTTPS.
- **Amazon VPC**: Provides the isolated network environment.
- **Internet Gateway**: Allows public subnet resources to access the Internet.
- **Application Load Balancer**: Distributes traffic to EC2 instances.
- **Amazon EC2**: Runs the backend application and APIs.
- **Auto Scaling Group**: Automatically adjusts the number of EC2 instances.
- **Amazon DocumentDB**: Stores document-based application data in private subnets.
- **Amazon CloudWatch**: Collects system metrics and logs.
- **CloudWatch Alarm**: Triggers alerts based on monitoring thresholds.
- **Amazon SNS**: Sends email notifications to administrators.
- **Cloudflare**: Manages DNS and protects the external access layer.

#### Component Design

- **Frontend**: The website is built and deployed on AWS Amplify.
- **DNS and HTTPS**: Cloudflare manages DNS; AWS Certificate Manager provides SSL/TLS.
- **Backend**: EC2 instances process LMS APIs and business logic for courses, lessons, users, learning progress, and submissions.
- **Database**: Amazon DocumentDB stores LMS data in private subnets and is not directly exposed to the Internet.
- **High Availability**: The system spans two Availability Zones to reduce downtime risk.
- **Monitoring**: CloudWatch collects metrics/logs, while CloudWatch Alarm and SNS send email alerts.

### 4. Technical Implementation

#### Implementation Phases

- **Phase 1 - Research and Architecture Design**: Analyze requirements, identify AWS services, and finalize the architecture diagram.
- **Phase 2 - Network and Security Setup**: Create VPC, public/private subnets, Internet Gateway, security groups, and DNS/HTTPS configuration.
- **Phase 3 - Application Deployment**: Deploy the frontend to AWS Amplify, deploy the backend to EC2, and place EC2 behind the ALB.
- **Phase 4 - Database and Replication**: Create Amazon DocumentDB in private subnets and configure replication across two Availability Zones.
- **Phase 5 - Monitoring and Notification**: Configure CloudWatch metrics/logs, CloudWatch Alarm, SNS topic, and email notifications.
- **Phase 6 - Testing and Optimization**: Test HTTPS access, APIs, database connectivity, scaling, failover, and alerts.

#### Technical Requirements

- Basic knowledge of AWS VPC, subnets, security groups, and routing.
- Experience deploying frontend applications with AWS Amplify.
- Ability to configure EC2, ALB, and Auto Scaling Group.
- Understanding of backend connectivity to Amazon DocumentDB.
- Knowledge of CloudWatch, CloudWatch Alarm, and Amazon SNS for monitoring.
- Ability to manage DNS with Cloudflare and map a domain to the system.

### 5. Timeline & Milestones

- **Week 1-2**: Analyze requirements, research architecture, and prepare design documentation.
- **Week 3-4**: Build VPC, subnets, routing, security groups, and DNS configuration.
- **Week 5-6**: Deploy the frontend on AWS Amplify and configure SSL/TLS.
- **Week 7-8**: Deploy backend on EC2, configure ALB and Auto Scaling Group.
- **Week 9-10**: Create DocumentDB, connect backend to database, and test data operations.
- **Week 11**: Configure CloudWatch, alarms, SNS, and email notifications.
- **Week 12**: Test the full system, optimize cost, and complete the report.

### 6. Budget Estimation

The following table is an estimate for a demo/internship environment, assuming deployment in **US East (N. Virginia)**, low traffic, small data volume, and no taxes included. For production deployment, the cost must be validated with **AWS Pricing Calculator** because pricing depends on region, instance configuration, and usage level.

| Service | Assumed configuration | Reference calculation | Estimated monthly cost |
|---|---:|---:|---:|
| AWS Amplify Hosting | 300 build minutes, 1 GB storage, 10 GB data out | Build + storage + transfer | $4.52 |
| Amazon EC2 | 2 small instances for LMS backend | 2 instances running 730 hours/month | $15.18 |
| Amazon EBS | 2 volumes, 20 GB each | 40 GB/month | $3.20 |
| Application Load Balancer | 1 ALB, low traffic | ALB hourly + low LCU usage | $18.20 |
| Amazon DocumentDB | Serverless/demo, minimum 0.5 DCU, 10 GB storage | DCU-hour + storage | $31.00 |
| Amazon CloudWatch | Basic logs, metrics, and alarms | Log ingestion + alarms | $2.00 |
| Amazon SNS | Low-volume email notifications | Basic notifications | $0.10 |
| AWS Certificate Manager | Public SSL/TLS certificate | No charge for public certificates used with AWS services | $0.00 |
| Data Transfer | Under the 100 GB/month free tier level | Low outbound traffic | $0.00 |
| **Total** |  |  | **$74.20/month** |
| **12-month estimate** |  |  | **$890.40/year** |

For a production environment with a multi-instance DocumentDB cluster, high traffic, or a larger amount of learning data, the cost will be significantly higher. During the internship, the project should use small configurations, limited test traffic, resource cleanup, and AWS Budget alerts to avoid unexpected costs.

### 7. Risk Assessment

#### Risk Matrix

- **Unexpected traffic spike**: High impact, medium probability.
- **EC2 instance failure**: Medium impact, medium probability.
- **Database overload or replication issue**: High impact, low probability.
- **Incorrect security group configuration**: High impact, medium probability.
- **Cost overrun**: Medium impact, medium probability.

#### Mitigation Strategies

- Use Auto Scaling Group to scale backend capacity automatically.
- Deploy across multiple Availability Zones to reduce downtime risk.
- Place DocumentDB in private subnets and restrict inbound access.
- Enable CloudWatch Alarm for CPU, memory, error requests, and instance health.
- Configure AWS Budget and review costs regularly.

#### Contingency Plans

- If an EC2 instance fails, Auto Scaling Group launches a replacement instance.
- If backend load is too high, increase instance size or adjust scaling policies.
- If the database has issues, check replicas and backups before recovery.
- If costs increase unexpectedly, reduce unnecessary resources and review traffic logs.

### 8. Expected Outcomes

#### Technical Improvements

- The website has HTTPS, proper DNS, and automated frontend deployment.
- Backend services can scale through ALB and Auto Scaling Group.
- The database is protected in private subnets and supports Multi-AZ replication.
- The system includes metrics/log monitoring and email-based alerting.

#### Long-term Value

This architecture can be extended into a real LMS platform with authentication, teacher/student roles, class management, document uploads, quizzes, notifications, CI/CD, and automated backups. It also provides a strong foundation for practicing important AWS topics during the internship.
