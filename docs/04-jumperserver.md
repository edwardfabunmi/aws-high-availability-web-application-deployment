# Step 4: Bastion Host / Jump Server

## Objective

A Bastion Host was created to provide controlled administrative access to the AWS environment.

## Configuration

The Bastion Host was deployed with:

Instance type: t2.micro
* Public subnet
* SSH key pair
* Appropriate security group

## User Data script

The User Data script was used to automatically configure the instance and install required components.

## Security Consideration

The Jumperserver acts as an entry point for administrative access rather than exposing application servers directly to the internet.

## Validation

Verify that:

* The Jumperserver is running.
* It is deployed in a public subnet.
* SSH access is working.
* The required security group is attached.
* User Data script completed successfully.
