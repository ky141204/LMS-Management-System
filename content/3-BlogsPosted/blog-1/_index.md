---
title: "Blog 1"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Building a Multi-Tenant Configuration System with Tagged Storage Patterns
---

> [!IMPORTANT]
> ### 🎯 Article goal
> In modern microservices architectures, multi-tenant configuration management remains one of the biggest operational challenges. This article provides a detailed guide to designing a high-performance, secure, event-driven configuration service on AWS, solving the cache TTL bottleneck and real-time data synchronization problem.
>
> * **Original article published at:** [AWS Study Group](https://awsstudygroup.com/2026/05/14/xay-dung-he-thong-cau-hinh-da-doi-tuong-thue-voi-cac-mau-luu-tru-duoc-gan-the/)

---

## 1. Major challenges of a Multi-Tenant Configuration System

When organizations scale SaaS (Software as a Service) systems to hundreds or thousands of tenants, traditional configuration management architectures often reveal two major gaps:

1. **Cache invalidation TTL latency**:
   * Tenant metadata changes faster than the cache TTL allows.
   * Traditional caching strategies force a trade-off: accept stale tenant context (causing data leakage or inaccurate feature flags), or constantly invalidate cache and increase load on the metadata service.
2. **Storage backend mismatch**:
   * Different configuration types have very different access patterns.
   * Frequently changing tenant configuration requires very high read/write throughput, which fits **Amazon DynamoDB**.
   * Shared system configuration or hierarchical settings that need versioning fit **AWS Systems Manager Parameter Store**.
   * Using a single backend for all configuration types significantly reduces operational performance.

---

## 2. Solution: Tagged Storage Pattern

This approach uses configuration key prefixes, such as `tenant_config_` or `param_config_`, to automatically route configuration requests to the most suitable AWS storage service through a **Config Strategy Factory** design.

![Overall architecture of the multi-tenant configuration system on AWS](images/multi_tenant_architecture.png)

### End-to-End Workflow

Based on the overall architecture diagram, request processing and update flow happen through 13 tightly connected steps:

1. **User authentication**: Client/Apps send the initial login request to **Amazon Cognito** `(1)`.
2. **Return JWT Token**: **Amazon Cognito** verifies the information and returns a JWT Token containing the custom tenant attribute (`custom:tenantId`) `(2)`.
3. **Send API request**: The client makes REST requests with the JWT Token passing through **AWS WAF** protection `(3)`.
4. **API Gateway routing**: The request continues to **AWS API Gateway (Public REST API)** `(4)`.
5. **Private integration**: **VPC Link V2** is used for secure integration `(5)`, routing traffic into the internal VPC network.
6. **Load routing**: **Application Load Balancer** receives the request and distributes it to the **REST API Controller** of the **Order Service** running on ECS Fargate `(6)`.
7. **Service discovery**: **Order Service** performs DNS Lookup through **AWS Cloud Map** `(7)` to find the Config Service address (`config-service.local:5000`).
8. **gRPC call**: The **gRPC Client** inside Order Service establishes a connection and calls `(8)` the **gRPC Controller** of the **Config Service** to optimize bandwidth.
9. **Strategy routing**: **Config Strategy Factory** `(9)` analyzes the prefix of the requested configuration:
   * If the prefix is `tenant_config_*` $\rightarrow$ choose **DynamoDB Strategy** and retrieve through a Gateway Endpoint with partition key `TENANT#{tenantId}`.
   * If the prefix is `param_config_*` $\rightarrow$ choose **SSM Strategy** and retrieve through an Interface Endpoint from **Parameter Store** encrypted by AWS KMS.
10. **Capture change events**: When a configuration change happens in Parameter Store, a change event `(10)` is sent to **Amazon EventBridge**.
11. **Trigger Lambda**: **Amazon EventBridge** detects the event and triggers `(11)` an **AWS Lambda** function.
12. **DNS lookup and cache refresh**: **AWS Lambda** discovers the service through Cloud Map `(12)` and calls `gRPC refresh() Direct` `(13)` directly to Config Service to immediately invalidate or refresh local cache without restarting containers.

---

## 3. Core components and architecture layers

The system is organized into 4 tightly connected layers to optimize performance and security:

### 💼 Layer 1: Storage layer - Multi-Backend Storage Strategy

* **Amazon DynamoDB (tenant-specific configuration)**:
  * Stores configuration unique to each customer, such as payment gateway settings and feature flags.
  * Uses a composite key schema: partition key `TENANT#{tenantId}` and sort key `CONFIG#{configType}`, providing absolute data isolation at the model level.
  * Provides single-digit millisecond retrieval latency.
* **AWS Systems Manager Parameter Store (shared configuration)**:
  * Manages relatively static but hierarchical parameters such as API endpoints and connection strings.
  * Uses path structure `/config-service/{tenantId}/{service}/{parameter}` to support batch retrieval, reducing the number of API calls from dozens to only one request during initialization.

### 🔌 Layer 2: Service layer - gRPC combined with Strategy Pattern

* Uses the **NestJS** framework together with high-performance **gRPC** for internal communication between microservices (east-west traffic).
* **Strategy Pattern** separates business logic from the actual storage implementation, making it easy to add new storage backends, such as S3 for large configuration files, without restructuring the entire core codebase.

### 🔐 Layer 3: Authentication layer - Extracting context from Cognito JWT Claims

* Cognito defines required custom attributes:
  * `custom:tenantId` (immutable) - tenant ID.
  * `custom:role` (changeable) - user role.
* **Secure design**: The configuration service never accepts `tenantId` directly from client API parameters. Instead, it decodes the JWT Token forwarded by API Gateway to extract `custom:tenantId`, completely preventing IDOR (Insecure Direct Object Reference) and cross-tenant data leakage risks.

### ⚡ Layer 4: Event-Driven Refresh layer

The solution fully solves the bottleneck of traditional cache TTL through an event-driven automatic update mechanism:

* Avoids continuous polling, which increases API call cost and creates information delay.
* Avoids service restarts that interrupt user sessions (zero downtime).
* Uses **Amazon EventBridge** + **AWS Lambda** to capture Parameter Store configuration update events and directly push cache invalidation signals to the gRPC API of Config Service. Cache synchronization across the ECS server cluster happens within only a few seconds.

---

> [!TIP]
> ### 💡 Summary of architecture value
> * **Absolute multi-tenant isolation**: Security from the Cognito JWT claim authentication layer to DynamoDB storage partitioning.
> * **Superior performance**: Flexible combination of gRPC performance and intelligent Strategy routing for each backend type.
> * **Zero-Downtime**: Event-driven cache refresh through EventBridge completely removes the need to restart services when new configuration updates occur.
