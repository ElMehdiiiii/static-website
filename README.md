# Hosting a Static Website on AWS

This project demonstrates how to host a static HTML web application on AWS using various AWS services. The resources and configurations used to deploy the web app on an EC2 instance are detailed below. 

## Project Overview

In this project, the following AWS services and configurations were utilized:


![Alt text](/Host_a_Static_Website_on_AWS.png)


1. **Virtual Private Cloud (VPC)**:
   - Configured with both public and private subnets across two different availability zones.

2. **Internet Gateway**:
   - Facilitates connectivity between VPC instances and the wider Internet.

3. **Security Groups**:
   - Act as a network firewall mechanism.

4. **Availability Zones**:
   - Leveraged two Availability Zones to enhance system reliability and fault tolerance.

5. **Public Subnets**:
   - Used for infrastructure components like the NAT Gateway and Application Load Balancer.

6. **EC2 Instance Connect Endpoint**:
   - Provides secure connections to assets within both public and private subnets.

7. **Private Subnets**:
   - Web servers (EC2 instances) positioned within Private Subnets for enhanced security.

8. **NAT Gateway**:
   - Enables instances in both the private Application and Data subnets to access the Internet.

9. **EC2 Instances**:
   - Hosted the website on EC2 Instances.

10. **Application Load Balancer**:
    - Distributes web traffic evenly to an Auto Scaling Group of EC2 instances across multiple Availability Zones.

11. **Auto Scaling Group**:
    - Automatically manages EC2 instances, ensuring website availability, scalability, fault tolerance, and elasticity.

12. **GitHub**:
    - Stored web files for version control and collaboration.

13. **Certificate Manager**:
    - Secures application communications.

14. **Simple Notification Service (SNS)**:
    - Alerts about activities within the Auto Scaling Group.

15. **Route 53**:
    - Registered the domain name and set up a DNS record.

## Deployment Script

The following Bash script automates the deployment of the static website on an EC2 instance:

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
git clone https://github.com/ElMehdiiiii/static-website.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R static-website/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf static-website

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd 

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## Steps to Deploy

1. **VPC Configuration**:
   - Create a VPC with public and private subnets in two availability zones.
   - Attach an Internet Gateway to the VPC.

2. **Security Groups**:
   - Create and configure Security Groups to allow necessary traffic.

3. **EC2 Instance Setup**:
   - Launch EC2 instances in the private subnets.
   - Use the provided script to install and configure the web server.

4. **Application Load Balancer**:
   - Set up an Application Load Balancer in the public subnets.
   - Configure target groups and listeners.

5. **Auto Scaling Group**:
   - Create an Auto Scaling Group to manage the EC2 instances.

6. **NAT Gateway**:
   - Deploy a NAT Gateway in the public subnet to enable internet access for instances in the private subnets.

7. **Domain and SSL Configuration**:
   - Register a domain name with Route 53 and set up DNS records.
   - Use AWS Certificate Manager to obtain and attach SSL certificates for secure communication.

8. **Monitoring and Alerts**:
   - Configure SNS to receive notifications about the Auto Scaling Group activities.

## GitHub Repository

The complete reference diagram, deployment scripts, and additional documentation can be found in the GitHub repository: [GitHub Repository](https://github.com/ElMehdiiiii/static-website)

## Conclusion

This project showcases a comprehensive setup to host a static website on AWS using a robust and scalable infrastructure. By following the provided steps and utilizing the script, you can easily deploy and manage your web application on AWS.
