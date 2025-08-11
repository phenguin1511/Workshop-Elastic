---
title: "Clean Up Resources"
date: 2025-08-10
weight: 5
chapter: false
pre: "<b>5.</b>"
---

## Clean Up Resources

After completing the lab, delete all created resources to avoid unnecessary costs.

---

### ✅ 1. Delete EC2 Instance
1. Go to **EC2** → **Instances**.
2. Select the **redis-bastion** instance.
3. Click **Instance state** → **Terminate instance**.
4. Choose **Yes, terminate** to confirm.

💡 *Note:*  
- Once terminated, the instance is permanently deleted and cannot be restored.  
- If you used an **Elastic IP** for the Bastion Host, remember to release it in **EC2 → Elastic IPs** to avoid ongoing charges.

---

### ✅ 2. Delete ElastiCache
1. Go to **ElastiCache** → **Redis OSS**.
2. Select the created Redis cluster → **Delete**.
3. Delete the **Subnet Group** if no longer needed:
   - Go to **ElastiCache** → **Subnet Groups** → select the group → **Delete**.

💡 *Note:*  
- Deleting the Redis cluster will remove all data stored in it.  
- If **automatic backups** are enabled, manually delete snapshots in **ElastiCache → Snapshots**.

---

### ✅ 3. Delete VPC and Related Components
1. Go to **VPC** → select **VPC redis-ha-vpc**.
2. Click **Actions** → **Delete VPC**.
3. Confirm the deletion.

💡 *Note:*  
- Deleting a VPC will **automatically delete** its related resources, including:
  - Route Tables
  - Internet Gateway (IGW)
  - Subnets (Public & Private)
  - Security Groups within the VPC
- If the VPC is associated with a **NAT Gateway**, delete the NAT Gateway first (since NAT GW incurs hourly charges).

---

## 🔍 Pre-Lab Exit Checklist

- [ ] All EC2 instances have been terminated.  
- [ ] Elastic IP released (if any).  
- [ ] Redis cluster and snapshots deleted.  
- [ ] Subnet Groups deleted.  
- [ ] NAT Gateway deleted (if any).  
- [ ] VPC and related resources deleted.
