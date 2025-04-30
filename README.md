# aws-scalable-infrastructure

# AWS Scalable Server Infrastructure (No Terraform)

This project demonstrates how to deploy a highly available, secure, and scalable server infrastructure on AWS **using only the AWS Management Console and Bash scripts (User Data)** — no Terraform or CloudFormation.

## 🧱 Architecture Overview

The architecture is designed with the following goals:
- High Availability: Spread across 2 Availability Zones (AZs)
- Security: EC2 instances live in private subnets
- Scalability: Auto Scaling Group (ASG) increases/decreases EC2 instances based on traffic
- Load Balancing: Application Load Balancer (ALB) handles inbound traffic
- Monitoring & Logging: CloudWatch integration (explained later)

### 🔧 Key AWS Components
| Component          | Role                                                   |
|--------------------|--------------------------------------------------------|
| VPC          | Isolated cloud network                                 |
| 2 Public Subnets | Host ALB and NAT Gateways                            |
| 2 Private Subnets | Host EC2 instances (managed by ASG)                 |
| ALB (Application Load Balancer) | Routes public traffic to EC2s       |
| Auto Scaling Group (ASG) | Scales EC2 instances in private subnets     |
| NAT Gateways   | Allow EC2s in private subnets to access the Internet   |
| Internet Gateway | Allows ALB to receive public traffic                 |

---

## 🗺️ Architecture Diagram

![Architecture Diagram](./architecture/VPC%20SET%20UP.drawio.png)

---

## ⚙️ Deployment Steps

> Each stage is documented in the `docs/` folder

1. VPC & Subnet Setup – `docs/01-vpc-setup.md`  
   - Create VPC, route tables, 2 public + 2 private subnets, NAT + Internet gateways

2. EC2, ALB, and ASG Setup – `docs/02-alb-asg-ec2.md`  
   - Create launch template with user data  
   - Set up target group, ALB in public subnets  
   - Attach ASG to ALB, spread across private subnets

3. Monitoring & Logging – `docs/03-monitoring-logging.md`  
   - Set up CloudWatch Logs  
   - Enable detailed monitoring on EC2

4. Full Flow Overview – `docs/04-full-architecture.md`  
   - Traffic enters via ALB → routed to EC2s in private subnets → EC2s can reach out via NAT

---

## 🚀 How It Works

- **Inbound**:  
  Internet → Internet Gateway → ALB (in public subnet) → Target Group → EC2 in private subnet

- **Outbound (from EC2)**:  
  EC2 → NAT Gateway (in public subnet) → Internet Gateway → Internet

---

## 🧰 Tools Used

- AWS Console (for manual setup)
- Bash Script via EC2 User Data
- Draw.io (for architecture diagram)

---

## 👨‍💻 Author

Cloud Infinistra  
📘 [https://dev.to/alex_cloud]  





