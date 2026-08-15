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

## 7.5 After Successful access confirmed from the web application server from the loadbalancer with Launch Template

After Successful access confirmed from the LoadBalancer, a lightweight Bash script was used to automatically download and deploy the frontend website onto the JumperServer.

This approach was used to automate the initial application setup whenever a new EC2 instance was launched.

The script performs the following tasks:

1. Updates the Ubuntu package repository.
2. Installs the `unzip` package.
3. Creates/uses the `webserver` directory.
4. Downloads the frontend template.
5. Extracts the downloaded ZIP file.
6. Copies the website files into the web server directory.

---

## Deployment Script

The application deployment was automated using the following Bash script:

```bash
#!/bin/bash

# ============================================
# Frontend Application Deployment
# ============================================

# Update package repository
echo "Updating package repository..."
sudo apt update -y

# Install unzip
echo "Installing unzip..."
sudo apt install unzip -y

# Navigate to the application directory
echo "Preparing application directory..."
cd /home/ubuntu/webserver

# Download frontend template
echo "Downloading frontend template..."

wget https://templatemo.com/tm-zip-files-2020/templatemo_520_highway.zip

# Extract frontend template
echo "Extracting frontend template..."

unzip templatemo_520_highway.zip

# Copy website files into the web server directory
echo "Deploying website files..."

sudo cp -r templatemo_520_highway/* /home/ubuntu/webserver

echo "Frontend deployment completed successfully."
