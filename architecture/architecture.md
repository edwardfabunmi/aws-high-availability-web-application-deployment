# AWS Architecture

## Overview

The application follows a highly available architecture where the Application Load Balancer distributes incoming traffic across EC2 instances running in private subnets.

The EC2 instances are managed by an Auto Scaling Group and share persistent storage through Amazon EFS.

Datadog monitors the infrastructure and sends alerts to Slack when defined thresholds are exceeded.

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


## VPC Architecture

```text
VPC
│
├── Availability Zone A
│   ├── Public Subnet A
│   └── Private Subnet A
│
└── Availability Zone B
    ├── Public Subnet B
    └── Private Subnet B
```

### Public Subnets
The public subnets host internet-facing resources such as:

* Application Load Balancer
* Bastion Host
* NAT Gateway

### Private Subnets
The private subnets host the application EC2 instances managed by the Auto Scaling Group.

### Storage Architecture
Amazon EFS provides shared persistent storage that can be accessed by multiple EC2 instances.

### Monitoring Architecture

```mermaid
flowchart TD
    A[EC2 Instances] --> B[Datadog Agent]
    B --> C[Datadog]
    C --> D[CPU Monitor]
    D --> E[Notification Rule]
    E --> F[Slack]
```
