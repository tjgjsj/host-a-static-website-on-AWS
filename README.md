![Alt text](/Host_a_Static_Website_on_AWS.png)



# Host a Static Website on AWS

This project demonstrates how to host a static HTML web application on Amazon Web Services (AWS) using various AWS resources. The project includes a detailed architecture to ensure high availability, fault tolerance, and security. This readme file provides an overview of the architecture, steps to deploy the web application, and a script for setting up the web server.

## Architecture Overview

The architecture is designed to ensure that the static web application is highly available, secure, and scalable. The key components and configurations are as follows:

1. **Virtual Private Cloud (VPC)**: Configured with both public and private subnets across two different availability zones.
2. **Internet Gateway**: Facilitates connectivity between VPC instances and the Internet.
3. **Security Groups**: Act as network firewalls to control traffic.
4. **Availability Zones**: Utilized to enhance reliability and fault tolerance.
5. **Public Subnets**: Host infrastructure components like the NAT Gateway and Application Load Balancer.
6. **EC2 Instance Connect Endpoint**: Provides secure connections to assets within both public and private subnets.
7. **Private Subnets**: Hosts web servers (EC2 instances) for enhanced security.
8. **NAT Gateway**: Allows instances in private subnets to access the Internet.
9. **EC2 Instances**: Hosts the static website.
10. **Application Load Balancer**: Distributes web traffic evenly to an Auto Scaling Group of EC2 instances across multiple availability zones.
11. **Auto Scaling Group**: Manages EC2 instances for availability, scalability, and fault tolerance.
12. **GitHub**: Used for version control and collaboration.
13. **Certificate Manager**: Secures application communications.
14. **Simple Notification Service (SNS)**: Sends alerts about activities within the Auto Scaling Group.
15. **Route 53**: Manages the domain name and DNS records.

## Deployment Steps

### Prerequisites

1. AWS account with the necessary permissions to create and manage the listed resources.
2. A registered domain name.

### Step-by-Step Guide

1. **Clone the GitHub Repository**: The repository contains the reference diagram and scripts needed for deployment.

   ```bash
   git clone https://github.com/tjgjsj/host-a-static-website-on-AWS.git
   ```

2. **Configure the VPC**: Set up a VPC with both public and private subnets across two availability zones.

3. **Deploy the Internet Gateway**: Attach it to the VPC to enable Internet access.

4. **Set Up Security Groups**: Configure them to allow traffic to and from the necessary ports.

5. **Create Public and Private Subnets**: Distribute them across two availability zones.

6. **Set Up the NAT Gateway**: Place it in the public subnet to allow private instances to access the Internet.

7. **Deploy EC2 Instances**: Launch instances in the private subnets to host the web application.

8. **Configure the Application Load Balancer**: Distribute traffic across the EC2 instances.

9. **Set Up Auto Scaling**: Ensure that the number of EC2 instances adjusts based on demand.

10. **Register Domain and Set Up DNS with Route 53**: Point the domain to the Application Load Balancer.

11. **Set Up Certificate Manager**: Secure your application communications.

12. **Configure SNS**: Receive alerts about the Auto Scaling Group activities.

### EC2 Instance Setup Script

Use the following script to set up your EC2 instance to serve the static web application using Apache HTTP Server.

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
git clone https://github.com/tjgjsj/host-a-static-website-on-AWS.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-AWS/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-AWS

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## Conclusion

This project provides a comprehensive setup for hosting a static HTML web application on AWS, utilizing various AWS resources to ensure high availability, security, and scalability. The provided script automates the deployment of the web server, simplifying the process of getting your static website online. For more detailed information, refer to the project repository on GitHub.
