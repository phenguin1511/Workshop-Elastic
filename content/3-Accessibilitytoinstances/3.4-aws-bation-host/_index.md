---
title: "Create Bastion Host"
date: 2025-08-10
weight: 2
chapter: false
pre: "<b>3.4.</b>"
---

## 1. Introduction

A **Bastion Host** is an EC2 instance placed in a **public subnet** that acts as an intermediary (jump host) to SSH/RDP into instances located in a **private subnet**.  
Using a Bastion Host helps limit the need to open direct access ports to the private subnet from the Internet.

---

## 2. Steps to Create a Bastion Host

1. Open **AWS Management Console** → **EC2** → **Launch Instance**.
   
   ![Launch Instance](/images/2.prerequisite/bation-host-1.png)

2. **Basic Configuration**:
   - **Name**: `redis-bastion`
   - **OS**: Amazon Linux 2 (well-suited for AWS environments)
   - **Instance type**: `t3.micro` (sufficient for intermediate SSH tasks)

   ![Instance Config](/images/2.prerequisite/bation-host-2.png)

3. **Networking**:
   - **Subnet**: Select a **Public Subnet** (e.g., `public-subnet-bastion`)
   - **Auto-assign Public IP**: Enable **Enable** to assign a Public IP
   - **Security Group**: Select `SG_Bastion` (already configured to allow SSH from the admin IP)

   ![Networking Config](/images/2.prerequisite/bation-host-3.png)

4. **Key pair**:
   - Create a new key pair or select an existing one to SSH into the instance.

   ![Key Pair](/images/2.prerequisite/bation-host-4.png)

5. Click **Launch Instance** to create.

---

## 3. After Creation

- The `redis-bastion` instance will appear in the **EC2 Instances** list with a *running* status.
- Use the selected key pair to SSH into the Bastion Host from the admin machine:

```bash
ssh -i <your-key.pem> ec2-user@<Public-IP-Bastion>
```
Here, <Public-IP-Bastion> is the IPv4 Public Address just assigned to the EC2 instance.


![Key Pair](/images/2.prerequisite/bation-host-5.png)

After running, you will get the following result:

![Key Pair](/images/2.prerequisite/bation-host-6.png)

To test if the connection works, try:
```bash
ping 8.8.8.8
crul http://google.com
```

## 4. Install Redis CLI
```bash
sudo dnf install -y tar gzip make gcc
curl -O http://download.redis.io/redis-stable.tar.gz
tar xzvf redis-stable.tar.gz
cd redis-stable
make
sudo make install

```
✅ After completion, check the redis-cli version:

```bash
redis-cli --version
```
![Key Pair](/images/2.prerequisite/bation-host-7.png)

💡 Technical Notes
SSH Security:
Only allow the admin IP to access port 22 (do not use 0.0.0.0/0 unless in a lab environment).

Session Management:
Consider using AWS Systems Manager Session Manager instead of SSH to reduce the need for opening port 22 to the Internet.

Cost:
Use a small instance type for the Bastion Host, and stop it when not in use to save costs.

Logging:
Consider enabling CloudWatch Logs or using Session Manager to record access history.