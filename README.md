Static Website Hosting on AWS EC2
This project involves hosting a static HTML web application on AWS, utilizing several AWS resources for enhanced security, availability, and scalability. Below is a detailed overview of the infrastructure used to deploy the web application.

Architecture Overview
The infrastructure is designed with high availability, fault tolerance, and security in mind. The deployment utilizes multiple AWS services, including VPC, EC2, ALB, Route 53, and more.

Key Components
Virtual Private Cloud (VPC) Configuration

Configured a VPC with both public and private subnets:
Two public subnets for the Application Load Balancer (ALB).
Two private subnets for the EC2 instances hosting the web server.
Internet Gateway

Deployed an Internet Gateway to enable communication between the VPC and the wider internet.
Security Groups

Established security groups as a firewall mechanism to control inbound and outbound traffic for the EC2 instances, NAT gateway, and ALB.
Availability Zones

Leveraged two availability zones to enhance the reliability and fault tolerance of the application.
Public Subnets

Used public subnets for resources like the NAT Gateway and Application Load Balancer (ALB).
EC2 Instance Connect Endpoint

Implemented EC2 Instance Connect for secure connection to resources within the VPC, defined by the CIDR block.
Private Subnets

Positioned the web server within the private subnet to enhance security, ensuring limited direct exposure to the public internet.
EC2 Instance for Web Hosting

Hosted the static HTML website on an EC2 instance.
Application Load Balancer (ALB) and Target Group

Deployed an Application Load Balancer and a target group to evenly distribute incoming web traffic across an Auto Scaling Group (ASG). The ASG automatically manages the EC2 instances, ensuring availability, scalability, fault tolerance, and elasticity.
Version Control

Stored the web application files on GitHub for version control and collaboration purposes.
Secured Communication

Secured the application’s communication using AWS Certificate Manager (ACM) to provide SSL/TLS certificates.
Domain Registration & DNS

Registered a domain name and set up DNS records using Route 53 to route traffic to the Application Load Balancer.


Deployment script
#!/bin/bash

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository to the current directory
git clone https://github.com/Godwin-svg/HTML-Website-on-an-EC2-Instance-1.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R HTML-Website-on-an-EC2-Instance-1/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf HTML-Website-on-an-EC2-Instance-1

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd 

# Start the Apache HTTP Server to serve web content
systemctl start httpd
