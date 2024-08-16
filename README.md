![Alt text](/Host_a_Static_Website_on_AWS.png)

---
# Host a Static Website on AWS - DevOps Project

## Project Overview

This project demonstrates how to host a static HTML web application on Amazon Web Services (AWS) by utilising various AWS services and infrastructure components. The project showcases a highly available, secure, and scalable web architecture deployed on EC2 instances within a Virtual Private Cloud (VPC). The project repository contains all the necessary scripts, configuration files, and documentation to replicate the deployment.

## Architecture Diagram

An architecture diagram depicting the setup and flow of the infrastructure can be found in the repository. This diagram illustrates the following components:

1. **Virtual Private Cloud (VPC)**: Configured with both public and private subnets across two different availability zones to ensure high availability and fault tolerance.
2. **Internet Gateway**: Facilitates connectivity between VPC instances and the wider internet.
3. **Security Groups**: Serve as a network firewall, controlling inbound and outbound traffic to the EC2 instances.
4. **Public Subnets**: Host infrastructure components like the NAT Gateway and Application Load Balancer.
5. **Private Subnets**: Host web servers (EC2 instances) for enhanced security.
6. **NAT Gateway**: Enables instances in private subnets to access the internet while maintaining security.
7. **Application Load Balancer**: Evenly distributes incoming web traffic across multiple EC2 instances in an Auto Scaling Group.
8. **Auto Scaling Group**: Automatically manages EC2 instances to ensure website availability, scalability, and fault tolerance.
9. **Amazon Route 53**: Provides domain name registration and DNS configuration.

## AWS Resources Used

- **EC2 Instances**: Host the static website and run the Apache HTTP Server.
- **VPC**: Provides isolated networking.
- **Subnets (Public and Private)**: Segregate resources for security and availability.
- **Internet Gateway**: Enables internet access for public subnets.
- **NAT Gateway**: Allows private subnet instances to reach the internet.
- **Security Groups**: Control traffic to and from EC2 instances.
- **Application Load Balancer**: Distributes traffic across multiple EC2 instances.
- **Auto Scaling Group**: Manages EC2 instances based on demand.
- **Amazon Certificate Manager**: Secures communications with SSL/TLS certificates.
- **Amazon SNS**: Sends notifications about activities in the Auto Scaling Group.
- **Amazon Route 53**: Manages DNS and domain name registration.

## Installation and Setup

Follow these steps to set up and deploy the static website:

### 1. Clone the Project Repository
Clone the GitHub repository containing the project files and scripts:

```bash
git clone https://github.com/MrStewartSalmon/host-a-static-website-on-aws.git
```

### 2. Configure AWS Infrastructure
Refer to the architecture diagram and deploy the AWS infrastructure components listed in the diagram. This includes creating a VPC, subnets, security groups, NAT gateway, and setting up the Application Load Balancer and Auto Scaling Group.

### 3. Launch EC2 Instances
Launch EC2 instances within the private subnets using the Auto Scaling Group. Ensure the instances are configured to run the startup script provided below.

### 4. EC2 Startup Script
The following startup script automates the setup of the Apache HTTP Server and deploys the web application from the GitHub repository:

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
git clone https://github.com/MrStewartSalmon/host-a-static-website-on-aws.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

### 5. Domain Name Configuration
Register a domain name using Amazon Route 53 and set up DNS records to point to the Application Load Balancer.

### 6. SSL/TLS Certificate
Secure your website using an SSL/TLS certificate from Amazon Certificate Manager. Attach the certificate to the Application Load Balancer.

### 7. Notifications and Monitoring
Set up Amazon SNS to receive notifications about activities within the Auto Scaling Group, such as instance launches or terminations.

## Repository Contents

- **Architecture Diagram**: Visual representation of the deployed infrastructure.
- **Startup Script**: Bash script to automate the installation of the web server and deployment of the website.
- **Documentation**: Detailed instructions on setting up each component of the infrastructure.
  
## Conclusion

This project provides a complete guide to hosting a static website on AWS with a focus on security, scalability, and high availability. By following the steps outlined in this repository, you can deploy a similar architecture and host your static website on AWS.

For further details, please refer to the repository files and the documentation provided within.

---
