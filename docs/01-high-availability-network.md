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


