---
title: "Create VPC and Subnet"
date: 2025-08-10
weight: 2
chapter: false
pre: "<b>2.2 </b>"
---

## 1. Create a VPC

To create a **VPC** (Virtual Private Cloud) on AWS, follow these steps:

1. Go to the **VPC Console** at:  
   [https://console.aws.amazon.com/vpc](https://console.aws.amazon.com/vpc)

2. In the left navigation menu, select **Your VPCs**.

   ![Your VPCs](/images/2.prerequisite/vpc-1.png)

3. Click **Create VPC**.

4. Configure the VPC settings as shown in the illustration:

   ![Create VPC](/images/2.prerequisite/vpc-2.png)

   - **Name tag**: `redis-ha-vpc`  
     > *The display name in the management console, recommended to follow the project’s naming convention.*
   - **IPv4 CIDR block**: `10.0.0.0/16`  
     > *The CIDR block defines the IP address range for the entire VPC. `/16` provides ~65,536 available IP addresses.*  
   - **Tenancy**: *Default*  
     > *Select Dedicated only if you need physically isolated hardware, which incurs higher costs.*

5. Click **Create VPC** to create the VPC.

   ![VPC Created](/images/2.prerequisite/vpc-3.png)

6. After creation, the new VPC will appear in the **Your VPCs** list with the status *Available*.

---

## 2. Create Subnets

A subnet is a subdivision of a VPC, with each subnet located in **one** Availability Zone (AZ).  
For deploying an HA (High Availability) system, you need to create multiple subnets in different AZs.

### Steps to create subnets

1. In the **VPC Console**, select **Subnets** in the left menu.

   ![Subnets Menu](/images/2.prerequisite/subnet-1.png)

2. Click **Create subnet**.

3. In the **VPC ID** field, choose the VPC you just created (`redis-ha-vpc`).

4. Create the following subnets one by one:

   **a. Subnet for AZ1**  
   - **Subnet name**: `AZ1`  
   - **Availability Zone**: choose AZ1 of your selected region  
   - **IPv4 CIDR block**: `10.0.1.0/24`  
     > *Provides 256 IP addresses for part of the workload in AZ1.*

   **b. Subnet for AZ2**  
   - **Subnet name**: `AZ2`  
   - **Availability Zone**: different from AZ1 and AZ3  
   - **IPv4 CIDR block**: `10.0.2.0/24`

   **c. Subnet for AZ3**  
   - **Subnet name**: `AZ3`  
   - **Availability Zone**: different from AZ1 and AZ2  
   - **IPv4 CIDR block**: `10.0.3.0/24`

   **d. Public Subnet** (for Bastion Host)  
   - **Subnet name**: `Public-Subnet`  
   - **Availability Zone**: same as AZ1 to optimize cost  
   - **IPv4 CIDR block**: `10.0.10.0/24`  
     > *The public subnet will be attached to an Internet Gateway to allow external connections.*

5. Click **Create subnet** after completing the configuration.

   ![Subnets Created](/images/2.prerequisite/subnet-2.png)

6. The result after successful creation:

   ![Subnets List](/images/2.prerequisite/subnet-3.png)

---

## 💡 Technical Notes

- **Plan IP addresses in advance**: Avoid overlapping CIDR blocks between subnets or with your existing network.
- **Separate public and private subnets**: Public subnets connect to the Internet Gateway; private subnets use a NAT Gateway/Bastion to access the internet.
- **High Availability (HA)**: Spread subnets across at least 2–3 AZs to improve fault tolerance if one AZ fails.
- **Naming convention**: Use consistent naming rules for easier management (e.g., `<env>-<purpose>-<az>`).
- **Use compact CIDR blocks**: Allocate only the IPs needed for each subnet to reserve space for future expansion.
