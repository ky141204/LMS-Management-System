---
title: "Blog 2"
date: 2026-07-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Securely Connecting AWS DevOps Agent to Private Services in Your VPC
---

> [!IMPORTANT]
> ### 🎯 Article goal
> This article explains how to set up a **Private Connection** that allows **AWS DevOps Agent** to securely access internal services running inside an Amazon VPC without exposing them to the public internet. This solves the security barrier when integrating MCP servers, self-hosted observability tools, and enterprise source control systems.
>
> * **Original article published at:** [AWS Study Group](https://awsstudygroup.com/2026/04/20/ket-noi-an-toan-aws-devops-agent-voi-cac-dich-vu-rieng-tu-trong-vpc-cua-ban/)

---

## 1. Introduction to AWS DevOps Agent

**AWS DevOps Agent** is an always-available operations teammate designed to:

* Resolve and **proactively prevent system incidents** before they happen.
* **Optimize application reliability and performance** in real time.
* Handle **SRE (Site Reliability Engineering)** tasks on demand across AWS, multi-cloud, and on-premises environments.
* Integrate with existing observability tools to correlate telemetry, source code, and deployment history, thereby significantly **reducing MTTR (Mean Time To Repair)**.

Many organizations extend **AWS DevOps Agent** with custom **Model Context Protocol (MCP)** tools, allowing the Agent to access internal systems such as:

* Private package repositories.
* Self-hosted observability platforms such as Grafana and Splunk.
* Internal documentation APIs.
* Source control systems such as **GitHub Enterprise** and **GitLab**.

The problem is that these services often run inside an **Amazon VPC** with **no public internet access**, so AWS DevOps Agent cannot reach them by default.

---

## 2. Solution: Private Connection

**Private Connection** for AWS DevOps Agent allows you to securely connect your **Agent Space** to services running inside a VPC or internal network **without exposing them to the public internet**.

Private Connection works with any integration that needs access to a private endpoint, including:

* Custom **MCP Servers**.
* Self-hosted **Grafana or Splunk** instances.
* Internal **source control** systems.

### How it works

At its core, AWS DevOps Agent uses **Amazon VPC Lattice** to establish this secure and private connectivity path. VPC Lattice is an application networking service that lets you connect, secure, and monitor communication between applications across VPCs, accounts, and compute types **without managing the underlying network infrastructure**.

When you create a private connection, the process happens in this order:

1. You provide the **VPC, Subnets**, and optionally **Security Groups** that have network connectivity to the destination service.
2. AWS DevOps Agent creates a service-managed **Resource Gateway** and provisions **Elastic Network Interfaces (ENIs)** in the specified subnets.
3. The Agent uses the Resource Gateway to **route traffic** to the IP address or DNS name of the destination service through the private network path.

> The Resource Gateway is fully managed by AWS DevOps Agent and appears as a **read-only resource** in your account. You do not need to configure or maintain it. The ENIs **do not accept inbound connections from the internet**, and you retain full control of traffic through your own Security Groups.

---

## 3. Overall architecture

![AWS DevOps Agent private connection architecture with VPC](images/devops_agent_private_connection.png)

### End-to-End Flow

| Step | Component | Description |
| :---: | :--- | :--- |
| **①** | **AWS DevOps Agent → Amazon VPC Lattice** | The Agent initiates the request and routes it through VPC Lattice. |
| **②** | **Amazon VPC Lattice → Resource Gateway** | VPC Lattice forwards the request to the service-managed Resource Gateway inside the Customer VPC. |
| **③** | **Resource Gateway → ENI (via IP/DNS)** | The Resource Gateway distributes traffic to ENIs in the Resource Gateway Subnet using the IP address or DNS name. |
| **④** | **ENI → Application (internal or on-premises)** | The ENI forwards the request to the target application inside the VPC or customer private network, protected by Security Group rules. |

*From the target service's perspective, the request originates from the **private IP address of the ENI** inside the VPC, with no exposure to the public internet.*

---

## 4. Security layers

> [!TIP]
> ### 🔐 Defense in Depth
>
> Private Connection is designed with **4 strong protection layers**:
>
> 1. **No public internet exposure**: All traffic between AWS DevOps Agent and the destination service stays on the **AWS internal network**. Your service never needs a public IP address or Internet Gateway.
> 2. **Read-only, service-controlled Resource Gateway**: The Resource Gateway is read-only in your account. It **can only be used by AWS DevOps Agent**; no other service or principal can route traffic through it. All actions are fully recorded in **AWS CloudTrail**.
> 3. **Customer-controlled Security Groups**: Traffic from DevOps Agent follows the **Outbound** rules of the Security Group associated with the Resource Gateway ENIs, and the **Inbound** rules of the destination service.
> 4. **Least-privilege service-linked role**: AWS DevOps Agent uses a tightly scoped service-linked role limited to resources tagged `AWSAIDevOpsManaged`. It **cannot access any other resources** in your account.
> 5. **DNS support**: You can reference services by DNS name. Note that DNS names need to be **publicly resolvable**.
