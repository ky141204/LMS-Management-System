---
title: "Event 1"
date: 2026-04-17
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# REFLECTION: FCAJ - HUTECH KICKOFF

---

> [!IMPORTANT]
>
> ### 🎯 Event Goal and Overview
>
> **FCAJ - HUTECH KICKOFF** is the launch event for academic activities, career orientation, and student connection in Information Technology at HUTECH. The event helps students understand the FCAJ community, the value of learning through workshops and real projects, and especially the direction of approaching cloud computing through the spirit of **First Cloud Journey**.

---

## 1. What is FCAJ?

### Event participation information

* **Format:** Offline.
* **Attendance location:** HUTECH University, E3 campus.

### General introduction

FCAJ is an academic community/group focused on helping students develop IT capabilities through learning, practice, and connection. Instead of only studying theory in class, students are encouraged to join practical activities such as workshops, team projects, technical sharing sessions, and career orientation events.

FCAJ is also connected with the spirit of **First Cloud Journey**: starting the cloud learning path from fundamental concepts, gradually approaching AWS services, and applying them through labs and real projects. This is suitable for beginners because AWS has many services, and without a roadmap, learners can easily feel overwhelmed.

### Role for students

FCAJ acts as an environment for:

* Learning beyond the formal curriculum.
* Approaching new technologies such as Cloud, DevOps, Serverless, and AI.
* Participating in practical projects.
* Connecting with peers, mentors, and seniors.
* Building self-learning and teamwork habits.

---

## 2. Main Content of the Event

### Activity orientation

During the kickoff, the organizing team introduced FCAJ's goals and activity direction. The focus is not only creating a student community, but also building an environment that helps learners move from fundamentals to practice.

The main points included:

* FCAJ activity roadmap.
* Training sessions, workshops, and technical seminars.
* Opportunities to participate in practical projects.
* Ways for students to develop both technical and soft skills.
* The importance of proactively joining a technology community.

### First Cloud Journey orientation

Based on the spirit of the **First Cloud Journey Kick off** video, I understood that learning cloud should not begin by memorizing as many AWS service names as possible. More importantly, learners need to understand what problem each service solves, when to use it, and how it works with other services.

An introductory cloud learning path can start with:

* **IAM:** Identity management, access control, and least privilege.
* **EC2:** Virtual servers and basic application deployment.
* **S3:** Object storage, static website hosting, and data storage.
* **VPC:** Private networking, subnets, route tables, and security groups.
* **RDS/DynamoDB:** Relational and NoSQL databases.
* **Lambda/API Gateway:** Serverless architecture and API development.
* **CloudWatch:** Logs, metrics, alarms, and observability.

### Sharing from speakers and the community

The event helped students realize that the IT industry changes quickly. If students only follow fixed classroom materials, they may lack practical experience. Joining communities, building projects, and practicing cloud are effective ways to reduce the gap between classroom knowledge and workplace requirements.

Important messages included:

* Students need to learn proactively instead of waiting for step-by-step instructions.
* Students should learn how to read official documentation and follow labs.
* Fundamentals should be understood before chasing new technologies.
* Students should ask questions, document errors, and share lessons learned.

---

## 3. Skills and Knowledge Emphasized

### Technical skills

Students need to build programming fundamentals and system thinking before going deep into a specific field. With cloud, learners should not only know how to deploy an application, but also understand security, networking, databases, monitoring, and cost.

Technical skills to practice include:

* Programming fundamentals and data structures.
* Understanding how web applications work from frontend to backend.
* Using Git/GitHub for source control.
* Becoming familiar with Linux command line and terminal.
* Practicing application deployment on cloud.
* Reading logs and handling basic errors.

### Foundational cloud skills

Through the First Cloud Journey orientation, I found several important cloud skills:

* Creating and securing an AWS account.
* Using IAM users, roles, and policies correctly.
* Creating S3 buckets and managing access.
* Deploying EC2 instances and configuring security groups.
* Understanding region, availability zone, and endpoint.
* Setting budget alarms for cost control.
* Cleaning up resources after workshops to avoid charges.

### Soft skills

Besides technical knowledge, the event also emphasized soft skills:

* Teamwork.
* Communication and idea presentation.
* Time management.
* Asking questions and giving feedback.
* Documenting the learning process.
* Sharing knowledge with the community.

---

## 4. Value of Joining the Community

Joining FCAJ brings many benefits:

* A learning environment beyond the classroom.
* Access to practical workshops.
* Opportunities to learn from seniors and peers.
* Wider networking in the technology field.
* More motivation through a community that grows together.

For broad topics such as AWS Cloud, community support is even more important. When studying alone, learners can get lost among too many services. In a community, students can follow a roadmap, ask questions when they face errors, and learn from others' experience.

---

## 5. Cloud Learning Roadmap Suggested by the Event

After joining the event and relating it to First Cloud Journey, I realized that cloud learning should be layered instead of random. A reasonable roadmap can be divided into the following stages.

### Stage 1: Understand Internet and web application fundamentals

Before learning AWS, students need to understand how a web application works. Concepts such as domain, DNS, HTTP/HTTPS, client-server, API, database, and authentication are foundations for understanding why cloud platforms need different service groups.

Without these concepts, AWS can feel confusing because learners may not know which part of the system EC2, S3, VPC, Route 53, API Gateway, or CloudFront is solving.

### Stage 2: Learn basic AWS services

After understanding web fundamentals, learners should begin with core services:

* **IAM** for access control.
* **S3** for file storage and static website hosting.
* **EC2** for virtual servers.
* **VPC** for cloud networking.
* **RDS or DynamoDB** for data storage.
* **CloudWatch** for logs and metrics.

At this stage, the goal is not to learn many services, but to understand how a basic cloud system works.

### Stage 3: Build a small project

When learners understand the basic services, they should build a small project. Examples include:

* Personal website hosted with S3 and CloudFront.
* Task management API using Lambda and API Gateway.
* Notes application using DynamoDB.
* Simple dashboard with logs and alarms in CloudWatch.

Small projects turn theory into experience. During deployment, learners will face permission errors, region mistakes, CORS issues, security group problems, or billing concerns. Fixing those issues builds deeper AWS understanding.

### Stage 4: Approach DevOps and automation

After manual deployment, the next step is learning automation through Infrastructure as Code and CI/CD. Learners can explore Terraform, AWS CDK, GitHub Actions, or CodePipeline. This is important because in enterprise environments, infrastructure should be managed as code for control and repeatability.

---

## 6. Example Application in a Student Project

A student who joins FCAJ and follows the First Cloud Journey direction can build a student event management project on AWS.

### Problem

The system allows students to view event lists, register for events, receive notifications, and check registration status.

### Proposed architecture

* **Frontend:** Static website hosted on Amazon S3 and delivered through CloudFront.
* **Backend:** API Gateway with AWS Lambda for registration logic.
* **Database:** DynamoDB for event and registration data.
* **Authentication:** Cognito can be added if login is required.
* **Monitoring:** CloudWatch logs and alarms for API errors.
* **Security:** IAM roles grant Lambda minimum permissions to access DynamoDB.

### Lessons from the project

Through this project, students can learn how AWS services work together. Instead of knowing each service separately, learners understand how to design a complete system from UI, backend, database, security, to monitoring.

---

## 7. Common Mistakes for AWS Beginners

The event helped me realize that making mistakes while learning cloud is normal. What matters is documenting and learning from them.

### IAM mistakes

Beginners often grant overly broad permissions or do not understand why they receive `AccessDenied`. This is why IAM should be learned carefully from the beginning. Every service calling another service needs the right role or policy.

### Region mistakes

Many learners create resources in one region but look for them in another, then think the resources are missing. When using AWS, checking the active region is always important.

### Networking mistakes

EC2 access problems are often related to security groups, route tables, public IPs, or key pairs. These errors are common but useful for understanding VPC.

### Cost mistakes

Some resources still cost money even when not used directly, such as running EC2 instances, NAT Gateways, Load Balancers, or databases. Cleanup after labs is a required habit.

### Lack of notes

If learners do not document errors and fixes, they can repeat the same mistakes. Documentation also helps share knowledge with the community, matching the learning spirit of FCAJ.

---

## 8. Lessons About Security and Cost When Learning Cloud

One lesson I took from the First Cloud Journey direction is that cloud learning must include security and cost awareness from the beginning.

### Security

Learners should avoid using the root account for daily work, enable MFA, and grant permissions based on least privilege. In workshops, broad permissions may be used for convenience, but real products require clear permission separation.

### Cost

Cloud can create costs if resources are left running. Learners need to understand:

* Which services charge by runtime.
* Which services charge by storage.
* Which services charge by request count.
* How to set AWS Budgets.
* How to clean up resources after labs.

This is practical because many beginners forget to delete EC2 instances, Load Balancers, NAT Gateways, or databases after practice.

---

## 9. Connection to Career Orientation

After the event, I saw that cloud is related to many career paths, not only DevOps Engineer.

### Backend Developer

Backend developers need to deploy APIs, connect databases, configure environments, and monitor logs. AWS Lambda, API Gateway, ECS, RDS, and CloudWatch are useful services.

### Frontend Developer

Frontend developers also need to understand website deployment, CDN, domain, HTTPS, and environment variables. S3, CloudFront, Route 53, and ACM are common services.

### DevOps/Cloud Engineer

This role is most directly related to cloud. DevOps engineers need to understand CI/CD, containers, monitoring, security, infrastructure as code, and cost optimization.

### AI/Data Engineer

Modern AI and data systems often run on cloud. Learners can approach S3, Glue, Athena, Redshift, SageMaker, Bedrock, or serverless services for data processing.

Because of this, joining FCAJ and starting First Cloud Journey helps students expand their career perspective instead of focusing on only one direction.

---

## 10. Personal Awareness

After joining the event, I realized that learning technology must be proactive and practical. Classroom knowledge is a foundation, but to be ready for work, students need to join workshops, build projects, and learn how to deploy real systems.

I also understood that cloud is not only for DevOps. Backend developers, frontend developers, AI engineers, data engineers, and security engineers all need some level of cloud knowledge. With AWS knowledge, students can deploy personal projects more professionally, host websites, build APIs, store data, monitor logs, and manage cost.

The most valuable point for me is the spirit of starting early. If students wait until internship or work to learn cloud, the pressure will be higher. If they start during school and practice a small part every week, after a few months they can build a useful foundation for real projects.

---

## 11. Personal Direction After the Event

After the kickoff, I set the following goals:

* Join more FCAJ activities.
* Review fundamentals of Web, Git, Linux, and Cloud.
* Practice basic AWS services such as IAM, S3, EC2, Lambda, and CloudWatch.
* Build a small project and deploy it on AWS.
* Document errors during practice to learn from them.
* Improve communication and teamwork skills.
* Explore more deeply the IT field I am interested in.

### Concrete action plan

In the coming time, I can divide the plan into small steps:

1. **Week 1:** Review IAM, create IAM users, enable MFA, and learn basic policies and least privilege.
2. **Week 2:** Set up AWS Budget, get familiar with AWS Management Console, CLI, and official documentation.
3. **Week 3:** Deploy a simple EC2 instance, configure security groups, key pairs, and SSH access.
4. **Week 4:** Build a basic VPC with public subnet, private subnet, route table, and Internet Gateway.
5. **Week 5:** Practice S3 static website hosting, lifecycle rules, and appropriate bucket permissions.
6. **Week 6:** Study AWS databases and compare RDS, DynamoDB, and DocumentDB for different use cases.
7. **Week 7:** Review security with IAM policies, MFA, security groups, credential reports, and cleanup habits.
8. **Week 8:** Practice CloudWatch logs, metrics, alarms, Auto Scaling, and observe how the system reacts to load changes.
9. **Week 9:** Build a small serverless function with Lambda, API Gateway, and basic queue/event integration.
10. **Week 10:** Learn CI/CD and deploy a sample application with GitHub Actions or AWS Developer Tools.
11. **Week 11:** Complete the capstone project by connecting frontend, backend, database, monitoring, and key failure tests.
12. **Week 12:** Write documentation, summarize errors, prepare the demo, present the result, and share lessons with the group.

This 12-week plan keeps cloud learning consistent from fundamentals and service practice to application deployment and capstone completion. The most important habits are cleaning up resources after each week, documenting lessons, and explaining the concepts in my own words.

---

> [!TIP]
>
> ### 💡 Lessons and General Awareness (Synthesis)
>
> Through FCAJ - HUTECH KICKOFF and the First Cloud Journey orientation, I learned several important lessons:
>
> 1. **Early orientation is important in IT.**
>    * A clear roadmap helps students learn more effectively and avoid being overwhelmed by too many technologies.
> 2. **Learning must go together with practice.**
>    * Cloud becomes easier to understand when learners deploy, face errors, read logs, and fix issues by themselves.
> 3. **Security and cost are foundations when learning AWS.**
>    * IAM, MFA, least privilege, budgets, and cleanup should be learned from the beginning.
> 4. **Community accelerates learning.**
>    * Joining FCAJ gives students an environment to discuss, practice, and grow together.

## Evidence photo

![Evidence photo from FCAJ - HUTECH KICKOFF](images/fcaj-hutech-kickoff-evidence.jpg)
