# aws-high-availability-web-application-deployment

## Project Overview
This project demonstrates the deployment of a highly available, scalable, and monitored web application on AWS.

The architecture was designed using multiple Availability Zones and AWS managed services to improve application availability, scalability, security, monitoring, and operational reliability.

The project includes:

* **Custom Amazon VPC**
* Public and private subnets across multiple Availability Zones
* Internet Gateway
* NAT Gateway
* Security Groups


* **Storage & Compute Infrastructure**
* **Amazon EFS** (with EFS Access Point)
* **Jump Server**
* **Amazon EC2** managed via Launch Template & Auto Scaling Group


* **Traffic Management & Routing**
* **Application Load Balancer** with Target Group
* **Amazon Route 53** (integrated with Namecheap DNS)


* **Security & Encryption**
* **AWS Certificate Manager (ACM)** for HTTPS/SSL termination


* **Monitoring & Alerting**
* **Datadog monitoring**
* **Slack alert notifications**

## Project Overview

The application follows a highly available architecture where the Application Load Balancer distributes incoming traffic across EC2 instances running in private subnets.

The EC2 instances are managed by an Auto Scaling Group and share persistent storage through Amazon EFS.

Datadog monitors the infrastructure and sends alerts to Slack when defined thresholds are exceeded.

## Architecture Flow

```mermaid
flowchart TD
    Internet([Internet]) --> Route53[Route 53 DNS / Domain]
    Route53 --> ALB[Application Load Balancer<br/>Port 80/443]

    subgraph Public_Subnets [Public Subnets]
        Bastion[Bastion Host / Jump Server]
        NAT[NAT Gateway]
        ALB
    end

    ALB --> EC2_A[EC2 Instance #1]
    ALB --> EC2_B[EC2 Instance #2]

    subgraph Private_Subnet_A [Private Subnet A]
        EC2_A
    end

    subgraph Private_Subnet_B [Private Subnet B]
        EC2_B
    end

    EC2_A --> EFS[(Amazon EFS<br/>Shared Storage)]
    EC2_B --> EFS

    %% Monitoring & Alerting Flow
    EC2_A -. Agent Data .-> Datadog[Datadog Monitoring]
    EC2_B -. Agent Data .-> Datadog
    Datadog --> Slack[Slack Alert Notifications]

    %% Styling
    style Public_Subnets fill:#f9f9f9,stroke:#333,stroke-dasharray: 5 5
    style Private_Subnet_A fill:#f0f7ff,stroke:#0066cc
    style Private_Subnet_B fill:#f0f7ff,stroke:#0066cc
```

## AWS Services Used

| Service | Purpose |
| :--- | :--- |
| **Amazon VPC** | Isolated network environment |
| **Amazon EC2** | Application and Bastion / Jumper Server instances |
| **Amazon EFS** | Shared persistent storage |
| **Auto Scaling** | Automatically manages EC2 capacity |
| **Application Load Balancer** | Distributes application traffic |
| **Target Group** | Manages application targets |
| **Route 53** | DNS management |
| **AWS Certificate Manager** | SSL/TLS certificate management |
| **Internet Gateway** | Internet connectivity for public resources |
| **NAT Gateway** | Outbound internet access from private subnets |
| **Security Groups** | Network-level access control |
| **IAM** | Access control for AWS resources |
| **Datadog** | Infrastructure monitoring |
| **Slack** | Monitoring notifications |
| **Namecheap** | Domain registration/DNS delegation |
