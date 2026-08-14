# Step 2: Amazon EFS

## Objective

Amazon Elastic File System was configured to provide shared persistent storage for the application servers.

This allows multiple EC2 instances to access the same file system.

## 1. Create EFS File System

An EFS file system was created inside the VPC.

## 2. Configure Mount Targets

Mount targets were configured in the required Availability Zones.

This allows EC2 instances running in different Availability Zones to access the shared storage.

## 3. Configure NFS Access

The required NFS traffic was configured through the security groups.

The relevant security groups were configured to allow NFS communication between the application instances and EFS.

## 4. Create EFS Access Point

An EFS Access Point was created to provide controlled access to the file system.
