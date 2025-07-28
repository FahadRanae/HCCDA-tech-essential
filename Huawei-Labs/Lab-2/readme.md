# Lab2
Compute Service Lab
# Huawei Cloud Compute Service Lab

This lab is designed to familiarize students with the process of remotely accessing and configuring virtual servers in the Huawei Cloud environment.

---

## Prerequisites

Log in to HUAWEI CLOUD.

Go to the **Lab Desktop** and open the **Google Chrome** browser to access the HUAWEI CLOUD login page. Select **IAM User Login**.

In the login dialog box, enter the assigned HUAWEI CLOUD lab account and password to log in to HUAWEI CLOUD, as shown in the following figure.

> **Note:** Replace with image if needed: `![Login Page](images/loginpage/your-image-name.png)`

---

## 1. Tasks

### 1.1 Creating a VPC

- Switch to the **management console** and select the **AP-Singapore** region.
- Navigate to:  
  `Service List > Networking > Virtual Private Cloud`.

#### Create a VPC:
- Name: `vpc-WP`
- Subnet: `subnet-WP`
- CIDR Block: `192.168.0.0/16`

> Note: System may assign a name like `vpc-Sandbox-voyager002`.

---

### 1.2 Creating ECSs

#### A. Windows ECS

- Navigate to:  
  `Service List > Compute > Elastic Cloud Server > Buy ECS`.

- Configure the following:
  - **Billing Mode**: Pay-per-use
  - **CPU Architecture**: x86
  - **vCPUs/RAM**: 2 vCPUs, 4 GB RAM
  - **Image**: Windows Server 2012 R2 Standard 64bit
  - **System Disk**: High I/O, 40 GB
  - **Login Mode**: Password (e.g., Huawei@1234)
  - **Name**: `ecs-windows`

#### B. Linux ECS

Repeat the same steps with the following differences:

- **Image**: CentOS 7.6 64bit
- **Name**: `ecs-linux`
- **EIP**: Auto Assign

---

### 1.3 Remote Login

#### Windows ECS:

1. Click `Remote Login` on the ECS console.
2. Send `Ctrl+Alt+Del`, then enter password.
3. Windows desktop indicates successful login.

#### Linux ECS:

1. Click `Remote Login > VNC`.
2. Username: `root`
3. Password: `Huawei@1234`
4. Successful login displays Linux terminal.

---

### 1.4 Modify ECS Specifications

To increase RAM or other specs:

1. Stop the ECS.
2. Click `More > Modify Specifications`.
3. Select new configuration (e.g., 8 GB RAM).
4. Submit and start the ECS again after it resizes.

---

## 2. Creating System Disk Images

### A. For Windows ECS

- Ensure:
  - DHCP is enabled.
  - Remote Desktop enabled.
  - `Cloudbase-Init` installed.
  
- Go to:  
  `Service List > Image Management Service > Private Images > Create Image`

- Choose `ecs-windows` as the source.

- Image Name: `image-windows2012`

### B. For Linux ECS

- Ensure:
  - DHCP enabled in `/etc/sysconfig/network-scripts/ifcfg-eth0`
  - `CloudResetPwdAgent` and `Cloud-Init` installed.
  - NIC rules removed from `/etc/udev/rules.d/70-persistent-net.rules`

- Create the image:
  - Name: `image-centos7.6`

---

## 3. Image Management Tasks

### 3.1 Modify Image

- Go to `Private Images > More > Modify Image`.
- Update name, OS, memory, etc.

### 3.2 Replicate Image

- Go to `Private Images > More > Replicate`.
- Confirm to replicate the image in the same region.

### 3.3 Apply Image to Create ECS

- Go to `Private Images > More > Apply for Server`.
- Select specifications and deploy the ECS.

---

## 4. Sharing Private Images Across Tenants

### 4.1 Get Project ID

- Log in with Main Huawei Cloud account.
- Go to `My Credentials > Project ID`.

### 4.2 Share Image

- Log in as Sandbox user.
- Go to `Private Images > More > Share`.
- Enter Project ID of the recipient.

### 4.3 Accept Image

- Log in with Main account.
- Go to `Private Images > Shared Images`.
- Accept the shared image.

### 4.4 Add to Shared With Tenants

- Go to `Shared with Tenants > Add Tenant`
- Paste Project ID and confirm.

---

## 5. Conclusion

This lab walks through the full cycle of working with Elastic Cloud Servers (ECS) on Huawei Cloud:

- Creating VPC and ECS
- Logging into Windows and Linux servers
- Creating and modifying system disk images
- Replicating and applying private images
- Sharing images across tenant accounts
- <img width="1125" height="325" alt="image" src="https://github.com/user-attachments/assets/f75f7ede-0cd2-4919-9756-d090916a194a" />
- <img width="1125" height="703" alt="image" src="https://github.com/user-attachments/assets/66eac1ef-6e1f-4ee8-952f-063a8ce864b9" />

- <img width="1125" height="430" alt="image" src="https://github.com/user-attachments/assets/e51021a9-5716-45bc-a64f-c65caf97ff82" />
- <img width="1125" height="1205" alt="image" src="https://github.com/user-attachments/assets/181c9fe8-f676-41b6-bd60-33c002cf8c8f" />

These hands-on tasks help students understand real-world cloud infrastructure management and automation on the Huawei Cloud platform.

---

