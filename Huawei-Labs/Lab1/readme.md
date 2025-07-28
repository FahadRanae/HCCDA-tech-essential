# Lab1
Deploying an Enterprise web

This lab guides you through the process of deploying a full-stack enterprise web application on Huawei Cloud. We will configure an Elastic Cloud Server (ECS) to host the frontend (Nginx) and backend (Tomcat), and set up a Relational Database Service (RDS) for the database.
# Deploying an Enterprise Web on Huawei Cloud

This guide demonstrates how to deploy an enterprise website on **Huawei Cloud** infrastructure using **Elastic Cloud Servers (ECS)**, **Relational Database Service (RDS)**, **LAMP stack**, **WordPress**, **Elastic Load Balancer (ELB)**, and **Auto Scaling (AS)**.

## 📌 Requirements

- Database nodes and service nodes must run on separate ECS instances.
- ECSs should automatically scale in or out based on traffic demand.

---

## 🔐 Prerequisites

1. **Log in to Huawei Cloud**
   - Go to the **Lab Desktop** and open **Google Chrome**.
   - Navigate to [HUAWEI CLOUD](https://www.huaweicloud.com/).
   - Select **IAM User Login**, then enter the assigned lab **account** and **password**.

⚠️ **Note:** Use only the credentials provided in the lab manual, not your personal Huawei account.

<img width="973" height="484" alt="image" src="https://github.com/user-attachments/assets/8743a300-2d5e-4683-b91e-b9cdb941dbf1" />



---

## 🚀 Tasks

### 1. Creating a Virtual Private Cloud (VPC)

- Switch to the **AP-Singapore** region.
- Navigate to: `Service List > Networking > Virtual Private Cloud`.
- Click **Create VPC** and configure:
  - **Name:** `vpc-mp`
  - Use default settings for the rest.
  - <img width="722" height="255" alt="image" src="https://github.com/user-attachments/assets/836a6fc0-e230-4901-ad52-3084f9e1ae25" />


### 2. Creating and Configuring a Security Group

- Navigate to: `Access Control > Security Groups`.
- Create a new group and click its name.
- Under **Inbound Rules**, add:
  - **Protocol & Port:** All
  - **Source IP:** `0.0.0.0/0`

### 3. Buying an ECS (Elastic Cloud Server)

- Go to: `Compute > Elastic Cloud Server > Buy ECS`.
- Set the following:
  - **Billing Mode:** Pay-per-use
  - **Region:** AP-Singapore
  - **CPU:** 1 vCPU, 1 GB RAM (`s6.small.1`)
  - **Image:** CentOS 7.6 (64-bit)
  - **Disk:** High I/O, 40 GB
  - **VPC & Security Group:** Use the ones created above
  - **EIP:** Auto assign (2 Mbps, Dynamic BGP)
  - **ECS Name:** `ecs-mp`
  - **Login Password:** e.g. `Huawei@123!`

### 4. Buying an RDS Instance (MySQL)

- Navigate to: `Database > Relational Database Service > Buy DB Instance`.
- Configuration:
  - **Engine:** MySQL 8.0
  - **Architecture:** Primary/Standby
  - **Specs:** 2 vCPUs, 4 GB RAM, Cloud SSD
  - **Billing:** Pay-per-use
  - **VPC, Security Group, Password:** Use previously created values
- Wait 6–10 minutes for creation.
- Note the **Floating IP** of the DB instance.
- <img width="1128" height="1338" alt="image" src="https://github.com/user-attachments/assets/7c752d87-00bb-455a-b558-f4419ee236b7" />


---

## 🧰 Setting Up LAMP Environment

### 1. Connect to ECS

- Go to `ECS Console > Remote Login`.
- Login as `root` using your ECS password.

### 2. Install LAMP Stack

```bash
yum install -y httpd php php-fpm php-mysql mysql
