# Step 8: Route 53 DNS Configuration
## Objective

Amazon Route 53 was used to manage DNS for the application.

## 1. Create Public Hosted Zone

A Public Hosted Zone was created for the domain.

## 2. Obtain Route 53 Nameservers

The Route 53 name servers were copied from AWS.

## 3. Configure Namecheap

The Route 53 name servers were configured in Namecheap.

The default Namecheap nameservers were replaced with the AWS Route 53 nameservers.

This delegated DNS management to Route 53.

## 4. Create Alias A Record

An Alias A Record was created to point the domain or subdomain to the Application Load Balancer.
