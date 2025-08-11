---
title: "Create IAM User"
date: 2025-08-10
weight: 2
chapter: false
pre: "<b>2.1</b>"
---

## Create an IAM User

1. Sign in to the **AWS Management Console** and open the IAM console at [IAM](https://console.aws.amazon.com/iam/).

   ![S3](/images/2.prerequisite/prerequisite-1.png)

2. In the IAM console, select **Users** from the left navigation menu.

   ![S3](/images/2.prerequisite/prerequisite-2.png)

3. Click **Create user** to add a new user.

   3.1 Enter the user name as **Elastic-Cache**.

   ![S3](/images/2.prerequisite/prerequisite-3.png)

4. In the **Permissions** section, choose **Attach existing policies directly**.

   4.1 Then click **Create Policy**.

   ![S3](/images/2.prerequisite/prerequisite-4.png)

5. In the **Policy Editor**, select **JSON** and paste the following code:

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
5. Then click **Next** to go to the **Review** section, and click **Create user**.