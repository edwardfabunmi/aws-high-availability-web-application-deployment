# Step 1: High Availability Network
The first stage was to create the networking infrastructure required for the highly available application.

## 1. Create the VPC
A custom VPC was created to isolate the application infrastructure.

The VPC contains four subnets distributed across Availability Zones.

* **VPC**
  * **Availability Zone A**
    * Public Subnet A
    * Private Subnet A
  * **Availability Zone B**
    * Public Subnet B
    * Private Subnet B
      
## 2. Create Public Subnets

Two public subnets were created:

* Public Subnet A
* Public Subnet B

The public subnets host internet-facing resources such as the Application Load Balancer and Bastion Host or JumperServer.

## 3. Create Private Subnets

Two private subnets were created:

* Private Subnet A
* Private Subnet B

The private subnets host application EC2 instances managed by the Auto Scaling Group.

## 4. Create Internet Gateway

An Internet Gateway was created and attached to the VPC.

It provides internet connectivity to resources located in the public subnets.

## 5. Create NAT Gateway

A NAT Gateway was deployed in a public subnet.

The NAT Gateway allows instances in the private subnets to initiate outbound internet connections without exposing those instances directly to the public internet.

## 6. Configure Route Tables

Two routing configurations were used.

Public Route Table

The public subnets were associated with the main route table.

The route table contains a default route through the Internet Gateway:

0.0.0.0/0 → Internet Gateway

## Private Route Table

A separate private route table was created for the private subnets.

The default route points to the NAT Gateway:

0.0.0.0/0 → NAT Gateway


### Network Verification

Verify that:

* **VPC:** The VPC exists.
* **Subnets:** All four subnets are available.
* **Public Routing:** Public subnets use the public route table.
* **Private Routing:** Private subnets use the private route table.
* **Internet Gateway:** The Internet Gateway is attached.
* **NAT Gateway:** The NAT Gateway is available.
* **Outbound Access:** Private instances can access outbound internet through the NAT Gateway.


