# Step 9: HTTPS / SSL Configuration
## Objective

AWS Certificate Manager was used to secure the application with HTTPS.

### 1. Request ACM Certificate

A public SSL/TLS certificate was requested through AWS Certificate Manager for the application domain.

### 2. DNS Validation

Domain ownership was validated using a DNS CNAME record in Route 53.

### 3. Certificate Status

After successful validation, the certificate status changed to:

Issued

### 4. Create HTTPS Listener

An HTTPS listener was created on the Application Load Balancer.

HTTPS
Port: 443

The ACM certificate was attached to the listener.

Traffic was then forwarded to the application Target Group.

### 5. Validate HTTPS

The application was validated using:

https://your-domain.com

After HTTPS was confirmed, the HTTP listener was configured to redirect HTTP traffic to HTTPS.

### Validation Checklist

- [ ] ACM certificate is issued
- [ ] DNS validation completed
- [ ] HTTPS listener created
- [ ] SSL certificate attached
- [ ] Traffic forwarded to Target Group
- [ ] HTTPS application loads successfully
