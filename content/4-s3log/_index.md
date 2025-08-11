---
title: "Connect and Test"
date: 2025-08-10
weight: 4
chapter: false
pre: "<b>4.</b>"
---

## 1. Connect to Redis

### Step 1: Start Redis
Open a **terminal** on EC2 and run:

```bash
redis-server

```

## 2: Connect to Redis from another terminal
Open another **terminal****, connect to EC2, then access the Redis shell:

```bash
redis-cli
```
## 3: Test storing and retrieving data
In **redis-cli**, enter:

```bash
set key1 "hello"
get key1
```
![Test](/images/2.prerequisite/test.png)

✅ If the result returns "hello", your Redis is running and can store/retrieve data successfully.

Technical Note
If you run set key1 "hello" or get key1 directly in the EC2 shell (without entering redis-cli), you will get the error command not found.

Reason: These are Redis commands, not Linux commands.

Correct way: Enter redis-cli first before using Redis commands.