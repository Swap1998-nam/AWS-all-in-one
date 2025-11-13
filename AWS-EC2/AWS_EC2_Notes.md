AWS EC2 (Elastic Compute Cloud)
Overview

Amazon EC2 (Elastic Compute Cloud) is one of the most popular and widely used AWS services.
It provides secure, resizable compute capacity in the cloud on a pay-as-you-go basis.

Key Features

🟢 Secure, resizable, and scalable service.

🟢 Pay-as-you-go pricing — you pay only for what you use.

🟢 Easily scalable — scale up or down within minutes.

🟢 Supports multiple instance types for different workloads.

Types of EC2 Instances

General Purpose – Balanced CPU, memory, and networking (e.g., t3, m5).

Compute Optimized – High-performance processors for compute-heavy workloads (e.g., c5).

Memory Optimized – Designed for large memory workloads (e.g., r5, x1).

Storage Optimized – High IOPS and throughput for storage-intensive tasks (e.g., i3, d2).

Accelerated Computing – Uses GPUs or FPGAs for high-performance computing and ML (e.g., p3, g4).

Key Components of EC2

AMI (Amazon Machine Image)
A pre-configured template containing OS, application server, and applications.
Used to launch instances quickly.

Instance Type
Defines the hardware configuration — CPU, memory, storage, and networking.

EBS Volume (Elastic Block Store)
Provides block-level storage for EC2 instances.

Persistent storage even after the instance stops.

Security Group (SG)

Virtual firewall controlling inbound and outbound traffic.

Operates at the instance level (Stateful).

Key Pair

Used for SSH (Linux) or RDP (Windows) access to EC2 instances.

Elastic IP

A static public IP address associated with your EC2 instance.

Remains the same even if the instance is stopped or restarted.

User Data Script

Used for automation and configuration during instance launch.

Example: Install Apache or Docker automatically on startup.

EC2 Networking Concepts

VPC (Virtual Private Cloud)
A private, isolated network environment to launch AWS resources.

Subnet

Logical subdivision of a VPC.

Can be public (internet-accessible) or private (internal).

Public IP

Accessible from the internet.

Assigned to instances in public subnets.

Private IP

Used for internal communication within a VPC.

Not accessible from the internet.

Elastic IP

Static, public IP address that doesn’t change across reboots.

Security Group (SG)

Acts as a stateful firewall for instances (remembers allowed traffic).

NACL (Network Access Control List)

Operates at the subnet level.

Stateless — rules must be defined for both inbound and outbound traffic.

Storage Options for EC2

EBS (Elastic Block Store)

Persistent block-level storage.

Used for OS, application data, and databases.

Automatically replicated within the same Availability Zone.

EFS (Elastic File System)

Shared file storage accessible by multiple EC2 instances simultaneously.

Scales automatically as you add or remove files.

Requires EC2s in the same region.

S3 (Simple Storage Service)

Object storage for backups, logs, media, and data archiving.

Highly durable (99.999999999%) and scalable.

Practical EC2 Tasks
1. Launch a Simple EC2 Instance

Use t2.micro instance (Free Tier eligible).

Select an AMI (e.g., Amazon Linux 2).

Configure key pair, security group, and storage.

2. Install a Web Server using User Data

Use the User Data field during launch to automate setup:

#!/bin/bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
echo "<h1>Welcome to AWS EC2 Web Server!</h1>" > /var/www/html/index.html

3. Create and Attach an EBS Volume

Create a new EBS volume (same Availability Zone as the EC2).

Attach the volume to your EC2 instance.

Connect via SSH and run:

sudo mkfs -t ext4 /dev/xvdf
sudo mkdir /data
sudo mount /dev/xvdf /data

4. Create an AMI (Backup or Clone)

Create an AMI of your EC2 instance to back up configuration or replicate environments.

5. IAM Role for EC2 to Access S3

Attach an IAM role with AmazonS3ReadOnlyAccess to your EC2 instance.

Example AWS CLI Commands:

aws s3 ls                      # List all S3 buckets
aws s3 ls s3://bucket-name     # List all objects in a specific bucket
aws s3 cp s3://bucket-name/file-name .  # Download a file

