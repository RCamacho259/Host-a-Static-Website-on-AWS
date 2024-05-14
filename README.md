**Project: Hosting a Static Website on AWS**


![Alt-text](/Host_a_Static_Website_on_AWS.png
---

### Overview

This project involves the deployment of a static HTML web application on Amazon Web Services (AWS). The infrastructure setup includes various AWS services such as Virtual Private Cloud (VPC), EC2 instances, Security Groups, Application Load Balancer, Route 53, etc. Below is a detailed description of the project's architecture and deployment process.

### Architecture

1. **Virtual Private Cloud (VPC)**:
   - Configured a VPC spanning across multiple Availability Zones (AZs) to ensure high availability and fault tolerance.
   - Created both public and private subnets within the VPC.

2. **Internet Gateway (IGW)**:
   - Deployed an Internet Gateway to enable connectivity between VPC instances and the Internet.

3. **Security Groups**:
   - Utilized Security Groups as a network firewall mechanism to control inbound and outbound traffic to EC2 instances.

4. **Availability Zones**:
   - Leveraged multiple Availability Zones to enhance system reliability and fault tolerance.

5. **EC2 Instances**:
   - Hosted the website on EC2 instances placed within private subnets for enhanced security.
   - Utilized EC2 Instance Connect Endpoint for secure connections to assets within both public and private subnets.

6. **NAT Gateway**:
   - Implemented NAT Gateway in the public subnets to allow instances in private subnets to access the Internet.

7. **Application Load Balancer (ALB)**:
   - Employed an ALB and a target group to evenly distribute web traffic to an Auto Scaling Group of EC2 instances across multiple Availability Zones.

8. **Auto Scaling Group (ASG)**:
   - Utilized an ASG to automatically manage EC2 instances, ensuring website availability, scalability, fault tolerance, and elasticity.

9. **Version Control**:
   - Stored web files on GitHub for version control and collaboration.

10. **Certificate Manager**:
    - Secured application communications using AWS Certificate Manager to manage SSL/TLS certificates.

11. **Simple Notification Service (SNS)**:
    - Configured SNS to alert about activities within the Auto Scaling Group.

12. **Route 53**:
    - Registered the domain name and set up a DNS record using Route 53 for easy access to the website.

### Deployment Script

```bash
#!/bin/bash

# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository to the current directory
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

### Conclusion

By following this deployment process and utilizing AWS services effectively, a static website can be successfully hosted on AWS with scalability, security, and high availability.

For detailed setup instructions and configuration parameters, refer to the project's GitHub repository and the accompanying documentation.
