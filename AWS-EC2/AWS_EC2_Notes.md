# AWS EC2 (Elastic Compute Cloud)

## Overview
Amazon EC2 (Elastic Compute Cloud) is one of the most popular and widely used AWS services.  
It provides secure, resizable compute capacity in the cloud on a **pay-as-you-go** basis.

### Key Features
- 🟢 **Secure, resizable, and scalable** service.  
- 🟢 **Pay-as-you-go** pricing — you pay only for what you use.  
- 🟢 **Easily scalable** — scale up or down within minutes.  
- 🟢 **Supports multiple instance types** for different workloads.

---

## Types of EC2 Instances
1. **General Purpose** – Balanced CPU, memory, and networking (e.g., `t3`, `m5`).
2. **Compute Optimized** – High-performance processors for compute-heavy workloads (e.g., `c5`).
3. **Memory Optimized** – Designed for large memory workloads (e.g., `r5`, `x1`).
4. **Storage Optimized** – High IOPS and throughput for storage-intensive tasks (e.g., `i3`, `d2`).
5. **Accelerated Computing** – Uses GPUs or FPGAs for high-performance computing and ML (e.g., `p3`, `g4`).

---

## Key Components of EC2

1. **AMI (Amazon Machine Image)**  
   A pre-configured template containing OS, application server, and applications.  
   Used to **launch instances** quickly.

2. **Instance Type**  
   Defines the **hardware configuration** — CPU, memory, storage, and networking.

3. **EBS Volume (Elastic Block Store)**  
   Provides **block-level storage** for EC2 instances.  
   - Persistent storage even after the instance stops.

4. **Security Group (SG)**  
   - Virtual firewall controlling **inbound and outbound** traffic.  
   - Operates at the **instance level** (Stateful).

5. **Key Pair**  
   - Used for **SSH (Linux)** or **RDP (Windows)** access to EC2 instances.

6. **Elastic IP**  
   - A **static public IP address** associated with your EC2 instance.  
   - Remains the same even if the instance is stopped or restarted.

7. **User Data Script**  
   - Used for **automation and configuration** during instance launch.  
   - Example: Install Apache or Docker automatically on startup.

---

## EC2 Networking Concepts

1. **VPC (Virtual Private Cloud)**  
   A private, isolated network environment to launch AWS resources.

2. **Subnet**  
   - Logical subdivision of a VPC.  
   - Can be **public** (internet-accessible) or **private** (internal).

3. **Public IP**  
   - Accessible from the internet.  
   - Assigned to instances in public subnets.

4. **Private IP**  
   - Used for internal communication within a VPC.  
   - Not accessible from the internet.

5. **Elastic IP**  
   - Static, public IP address that doesn’t change across reboots.

6. **Security Group (SG)**  
   - Acts as a **stateful firewall** for instances (remembers allowed traffic).

7. **NACL (Network Access Control List)**  
   - Operates at the **subnet level**.  
   - **Stateless** — rules must be defined for both inbound and outbound traffic.

---

## Storage Options for EC2

1. **EBS (Elastic Block Store)**  
   - Persistent **block-level storage**.  
   - Used for OS, application data, and databases.  
   - Automatically replicated within the same Availability Zone.

2. **EFS (Elastic File System)**  
   - **Shared file storage** accessible by multiple EC2 instances simultaneously.  
   - Scales automatically as you add or remove files.  
   - Requires EC2s in the same region.

3. **S3 (Simple Storage Service)**  
   - **Object storage** for backups, logs, media, and data archiving.  
   - Highly durable (99.999999999%) and scalable.

---

## Practical EC2 Tasks

### 1. Launch a Simple EC2 Instance
- Use `t2.micro` instance (Free Tier eligible).
- Select an AMI (e.g., Amazon Linux 2).
- Configure key pair, security group, and storage.

---

### 2. Install a Web Server using User Data
Use the **User Data** field during launch to automate setup:

```bash
#!/bin/bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
echo "<h1>Welcome to AWS EC2 Web Server!</h1>" > /var/www/html/index.html

# EC2 Storage and IAM Role Tasks

## 3. Create and Attach an EBS Volume

**Steps:**

1. Create a new **EBS volume** (ensure it’s in the same Availability Zone as your EC2 instance).  
2. Attach the newly created volume to your EC2 instance.  
3. Connect to the instance via SSH and execute the following commands:

```bash
sudo mkfs -t ext4 /dev/xvdf
sudo mkdir /data
sudo mount /dev/xvdf /data


# EC2 Image and IAM Role Configuration

## 4. Create an AMI (Backup or Clone)

**Purpose:**  
An Amazon Machine Image (AMI) allows you to back up your EC2 instance or replicate it to create identical environments.

**Steps:**

1. Open the **EC2 Console** → **Instances**.  
2. Select your instance → click **Actions → Image and templates → Create image**.  
3. Enter a name and description for your AMI.  
4. Choose whether to include the attached volumes.  
5. Click **Create Image**.  
6. Once created, check it under **AMIs** in the EC2 sidebar.  

**To launch a new instance from AMI:**

1. Go to **AMIs** → select your image → click **Launch instance from image**.  
2. Configure instance details, storage, and security group as required.  
3. Launch the new instance.

---

## 5. IAM Role for EC2 to Access S3

**Purpose:**  
IAM Roles enable your EC2 instances to access AWS services securely without storing access keys.

**Steps:**

1. Go to **IAM Console → Roles → Create role**.  
2. Choose **AWS service** and select **EC2**.  
3. Attach the policy:  
   - `AmazonS3ReadOnlyAccess` (for read-only access)  
4. Name your role and create it.  
5. Attach the role to your EC2 instance:  
   - In **EC2 Console → Instances → Select instance → Actions → Security → Modify IAM Role**  
   - Choose your newly created role.

**Verify S3 Access (from EC2 terminal):**

```bash
aws s3 ls                      # List all S3 buckets
aws s3 ls s3://bucket-name     # List all objects in a specific bucket
aws s3 cp s3://bucket-name/file-name .  # Download a file

