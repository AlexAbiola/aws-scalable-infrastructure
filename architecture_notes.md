# 🏗️ Architecture Notes

This document explains the architecture design used in this AWS scalable infrastructure project.

---

## 🌐 Overview

The setup is designed for high availability and scalability using AWS core services across **two Availability Zones (AZs)**. It follows a typical **3-tier architecture** pattern with public and private subnets.

---

## 🖼️ Architecture Diagram

- ![AWS Architecture Diagram](../VPC%20SET%20UP.drawio.png)
- [Click here to view on Google Drive](https://drive.google.com/file/d/1z1mtQzpXrv381BDmvyd16H10r4X1x_Dm/view?usp=drive_link)

---

## 📦 Components Breakdown

- **VPC (Virtual Private Cloud):** Isolated network where all AWS resources live.
- **2 Public Subnets:** One in each AZ. Hosts NAT Gateways and ALB (Application Load Balancer).
- **2 Private Subnets:** Hosts EC2 instances launched via Auto Scaling Group (ASG).
- **Internet Gateway:** Allows internet traffic into the VPC through the ALB.
- **NAT Gateways:** Allow instances in private subnets to access the internet without being exposed.
- **Application Load Balancer (ALB):** Accepts incoming traffic from the user and routes it to healthy instances in the ASG.
- **Auto Scaling Group (ASG):** Automatically handles instance scaling across private subnets.

---

## 🔁 Traffic Flow

1. **User** sends a request via browser.
2. Traffic hits the **Internet Gateway**.
3. Routed to the **ALB** in a **public subnet**.
4. ALB forwards traffic to **EC2 instances in private subnets** managed by ASG.
5. If the EC2s need to access the internet (e.g., for updates), they go out via the **NAT Gateway**.

---

## 📌 Notes

- **ALB lives in public subnets** because it must be internet-facing.
- **EC2s live in private subnets** for security.
- **NAT Gateway** must be in public subnet, with route tables configured to allow private subnets to reach the internet through it.
- Design ensures **redundancy and failover** across two AZs.

---

