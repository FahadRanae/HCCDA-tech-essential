# Lab 3
Storage Service Practice
# Storage Services Practice

## 1. Elastic Volume Service (EVS)

### 1.1 About This Exercise
EVS provides persistent block storage for ECSs and BMSs with high availability, durability, and low latency through data redundancy and cache acceleration techniques.

### 1.2 Objectives
- Purchase EVS disks
- Attach EVS disks
- Initialize EVS disks on Windows and Linux servers
- Use EVS snapshots

### 1.3 Tasks

#### 1.3.1 Attaching EVS Disk to Windows ECS
1. **Purchase EVS Disk**
   - Navigate to Elastic Volume Service
   - Configure disk parameters (High I/O, 20GB, AZ1)
   - Submit and verify disk creation

2. **Attach Non-shared EVS Disk**
   - Select disk in "Available" state
   - Attach to target Windows ECS (ecs-vivi)
   - Verify disk status changes to "In-use"

3. **Initialize EVS Disk**
   - Remote login to ECS
   - Use Disk Management to bring disk online
   - Initialize as MBR/GPT
   - Create new simple volume with quick format

4. **Verification**
   - Create test file (test.txt)
   - Detach disk and attach to second ECS (ecs-test)
   - Verify file persistence

#### 1.3.2 Attaching EVS Disk to Linux ECS
1. Create Linux ECS (CentOS 7.6)
2. Purchase and attach EVS disk
3. Partition and format disk using fdisk
4. Mount filesystem and verify

#### 1.3.3 Using Snapshots (Optional)
1. Create test file on Linux ECS
2. Create snapshot of EVS disk
3. Create new disk from snapshot
4. Attach and verify data persistence

## 2. Object Storage Service (OBS)

### 2.1 About This Exercise
OBS provides scalable, secure cloud storage for unstructured data accessible via REST APIs.

### 2.2 Objectives
- Create buckets and folders
- Upload/download files
- Delete files/folders/buckets

### 2.3 Tasks
1. **Create Bucket**
   - Region: AP-Singapore
   - Storage Class: Standard
   - Policy: Private
   - Name: test-vivi

2. **Upload Files**
   - Navigate to bucket
   - Upload sample files (e.g., background.jpg)

3. **Download Files**
   - Select and download files to local system

4. **Delete Files/Buckets**
   - Remove test files
   - Delete bucket when complete

## 3. Scalable File Service (SFS)

### 3.1 About This Exercise
SFS provides shared file storage accessible by multiple ECSs/BMSs/containers.

### 3.2 Objectives
- Create SFS Turbo file system
- Mount on Linux/Windows servers
- Enable cross-VPC sharing

### 3.3 Tasks

#### 3.3.1 Create SFS Turbo File System
1. **Prerequisites**
   - Create VPC (vpc-mp)
   - Provision Linux/Windows ECS with EIPs

2. **Create File System**
   - Type: General
   - Protocol: NFS
   - Capacity: 500GB
   - VPC: vpc-mp
   - Name: sfs-mp

#### 3.3.2 Mount on Linux ECS
1. Install NFS utilities
2. Create mount directory (/localfolder)
3. Mount file system
4. Configure automatic mounting via fstab
5. Create test file for verification

#### 3.3.3 Mount on Windows ECS
1. Install NFS client via Server Manager
2. Configure NFS client properties
3. Mount file system using command prompt
4. Verify cross-ECS file sharing

## Prerequisites
- HUAWEI CLOUD account credentials
- AP-Singapore region access
- Basic familiarity with ECS management

## Notes
- Replace placeholder names (vivi, mp) with your assigned account identifiers
- All resources should be created in AP-Singapore region
- Clean up resources after exercise completion to avoid charges
- <img width="1125" height="923" alt="image" src="https://github.com/user-attachments/assets/635270a8-b60c-4153-b3be-f7cb89e2e2c8" />
- <img width="1125" height="544" alt="image" src="https://github.com/user-attachments/assets/2ef745fb-fd26-4e53-aac9-0109f1605f00" />
