# aws-2tier-architecture-python-app
Deployment of a secure 2-Tier Architecture on AWS with VPC, Auto Scaling, Bastion Host, Load Balancer, and Python application.
🏗️ Architecture Overview

VPC with 2 Public and 2 Private Subnets (in different AZs for HA)

Internet Gateway (IGW) and NAT Gateway with Elastic IP

Auto Scaling Group with Launch Template to deploy EC2 instances in private subnets

Bastion Host in the public subnet for secure SSH access to private EC2 instances

Application Load Balancer (ALB) in public subnet to route traffic to private instances

Python Application installed on private EC2 instances

📋 Steps to Deploy
1. Create VPC

Use VPC Wizard (More Options) to create:

2 Public Subnets

2 Private Subnets

Internet Gateway

NAT Gateway with Elastic IP

2. Launch Private EC2 Instances

Create a Launch Template for EC2.

Deploy an Auto Scaling Group (ASG) with 2 EC2 instances in private subnets.

3. Setup Bastion Host

Launch an EC2 instance in a Public Subnet (Ubuntu/ Amazon Linux).

Enable SSH (port 22) for secure access.

Copy the .pem key file from local machine to Bastion Host.

SSH into Bastion Host → SSH into Private EC2 instances.

4. Install Python Application

SSH into private EC2 instance (via Bastion).

Install Python & dependencies:

sudo apt update -y
sudo apt install python3 -y


5. Configure Load Balancer

Create a Target Group and register private EC2 instances.

Create an Application Load Balancer (ALB) in public subnet.

Attach the target group to the ALB.

6. Access Application

Once ALB is active, copy the DNS Name from ALB.

Paste into browser to access the Python app.

Load Balancer ensures traffic distribution between 2 private instances.

🖼️ Architecture Diagram
   Internet
      |
   [ALB - Public Subnet]
      |
   -------------------------
   |                       |
[EC2-1 Private]       [EC2-2 Private]
   |                       |
 (Python App)           (Python App)
   
Bastion Host (Public Subnet) → Secure SSH into Private Instances  

⚙️ Tech Stack

AWS VPC (Networking)

EC2 (ASG, Launch Templates)

NAT Gateway, IGW, Bastion Host

Application Load Balancer (ALB)

Python (Application Layer)

✅ Features

Secure access to private instances via Bastion Host

High Availability with Multi-AZ setup

Auto Scaling for resilience & scalability

Load Balancing for traffic distribution

🔮 Future Improvements

Add RDS for database layer (3-Tier Architecture).

Use Terraform/CloudFormation for IaC deployment.

Integrate CI/CD pipeline for automated deployments.

📌 Author

👤 Mohammed Zeeshan Pasha
