---
title : "Tạo User IAM"
date :  2025-08-10 
weight : 2 
chapter : false
pre : " <b>2.1 </b> "
---

Tạo người dùng IAM

1. Đăng nhập vào Bảng điều khiển quản lý AWS và mở bảng điều khiển IAM tại [IAM](https://console.aws.amazon.com/iam/).

![S3](/images/2.prerequisite/prerequisite-1.png)

2. Trong bảng điều khiển IAM, chọn **Users** trên thanh menu bên trái.

![S3](/images/2.prerequisite/prerequisite-2.png)

3. Chọn **Create user** để tạo user mới.

  3.1 Nhập tên User là **Elastic-Cache**

![S3](/images/2.prerequisite/prerequisite-3.png)

4. Ở phần **Permission** chọn **Attach existing policies directly**

4.1 Sau đó chọn **Create Policy**

![S3](/images/2.prerequisite/prerequisite-4.png)


Ở phần **Policy Editor** chọn JSON và nhập đoạn code sau:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "EC2BastionAccess",
            "Effect": "Allow",
            "Action": [
                "ec2:Describe*",
                "ec2:RunInstances",
                "ec2:TerminateInstances",
                "ec2:StartInstances",
                "ec2:StopInstances",
                "ec2:RebootInstances",
                "ec2:CreateSecurityGroup",
                "ec2:AuthorizeSecurityGroupIngress",
                "ec2:AuthorizeSecurityGroupEgress",
                "ec2:RevokeSecurityGroupIngress",
                "ec2:RevokeSecurityGroupEgress",
                "ec2:CreateTags"
            ],
            "Resource": "*"
        },
        {
            "Sid": "VPCAndSubnetAccess",
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeVpcs",
                "ec2:DescribeSubnets",
                "ec2:DescribeRouteTables",
                "ec2:DescribeInternetGateways",
                "ec2:CreateSubnet",
                "ec2:DeleteSubnet",
                "ec2:CreateRouteTable",
                "ec2:AssociateRouteTable",
                "ec2:CreateInternetGateway",
                "ec2:AttachInternetGateway"
            ],
            "Resource": "*"
        },
        {
            "Sid": "ElastiCacheClusterAccess",
            "Effect": "Allow",
            "Action": [
                "elasticache:CreateCacheCluster",
                "elasticache:DeleteCacheCluster",
                "elasticache:ModifyCacheCluster",
                "elasticache:DescribeCacheClusters",
                "elasticache:CreateReplicationGroup",
                "elasticache:DeleteReplicationGroup",
                "elasticache:ModifyReplicationGroup",
                "elasticache:DescribeReplicationGroups",
                "elasticache:CreateCacheSubnetGroup",
                "elasticache:DeleteCacheSubnetGroup",
                "elasticache:DescribeCacheSubnetGroups",
                "elasticache:CreateSnapshot",
                "elasticache:DeleteSnapshot",
                "elasticache:DescribeSnapshots",
                "elasticache:ListTagsForResource",
                "elasticache:AddTagsToResource",
                "elasticache:RemoveTagsFromResource"
            ],
            "Resource": "*"
        },
        {
            "Sid": "CloudWatchAccess",
            "Effect": "Allow",
            "Action": [
                "cloudwatch:DescribeAlarms",
                "cloudwatch:PutMetricAlarm",
                "cloudwatch:DeleteAlarms",
                "cloudwatch:GetMetricStatistics",
                "cloudwatch:ListMetrics"
            ],
            "Resource": "*"
        },
        {
            "Sid": "S3BackupAccess",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::<your-backup-bucket>",
                "arn:aws:s3:::<your-backup-bucket>/*"
            ]
        },
        {
            "Sid": "IAMReadOnly",
            "Effect": "Allow",
            "Action": [
                "iam:ListRoles",
                "iam:ListUsers",
                "iam:GetRole",
                "iam:GetUser"
            ],
            "Resource": "*"
        }
    ]
}
```
5. Sau đó nhấn Next tới phần **Review** và nhấn **Create user**