---
title : "5.4.2 - Create IAM Roles"
date : 2026-03-25
weight : 2
chapter : false
pre : " <b> 5.4.2. </b> "
---

## Step-by-Step Guide: Create IAM Roles

### Objective
Create IAM roles that will be attached to users and used for service-to-service authentication. Roles will have the policies we created in 5.4.1.

---

## Background: Roles vs Policies

- **Policies** define WHAT actions are allowed (permissions)
- **Roles** are containers for policies that can be assumed by users, applications, or services

---

## Step 1: Open IAM Roles Console

1. In AWS IAM Console, on the left menu, click **Roles**
2. You'll see the roles dashboard with existing roles (if any)
3. Click **Create role** button

![](/images/5-Workshops/lab2/task2/step1.png)

---

## Step 2: Create Provider Role

### Step 2.1: Choose Trusted Entity

1. You're on **Select trusted entity** step
2. Keep the default: **AWS service** is selected
3. In the "Use case" section, click on **EC2**
   > This is just for now; we'll verify it can be used by users

4. Click **Next** button

![](/images/5-Workshops/lab2/task2/step2.png)

---

### Step 2.2: Add Permissions to Role

1. You're now on **Add permissions** step
2. In the search box, type: `EvDataProviderPolicy`
3. Check the box ✓ next to **EvDataProviderPolicy**
4. Click **Next** button

![](/images/5-Workshops/lab2/task2/step2.2.png)

---

### Step 2.3: Name the Role

1. You're on **Name, review, and create** step
2. In **Role name**, enter: `EvDataProviderRole`
3. In **Description**, enter: `Role for data providers to upload and manage EV datasets`
4. Leave **Maximum session duration** as default (1 hour)
5. Click **Create role** button


---

### Step 2.4: Update Trust Relationship

After creating the role, we need to allow users to assume this role:

1. Click on the new **EvDataProviderRole** from the roles list
2. Click the **Trust relationships** tab
3. Click **Edit trust policy** button


---

### Step 2.5: Modify Trust Policy

1. Replace the JSON with this trust policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "cognito-idp.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    },
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    },
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::ACCOUNT-ID:root"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

> **Note:** Replace `ACCOUNT-ID` with your AWS account ID

2. Click **Update policy** button


---

## Step 3: Create Consumer Role (Similar Process)

### Step 3.1: Create Consumer Role

1. Click **Create role** button
2. Select **AWS service** → **EC2** (again, just for now)
3. Click **Next**


---

### Step 3.2: Add Consumer Policy

1. Search for: `EvDataConsumerPolicy`
2. Check ✓ the box next to it
3. Click **Next**


---

### Step 3.3: Name Consumer Role

1. In **Role name**, enter: `EvDataConsumerRole`
2. In **Description**, enter: `Role for data consumers to download and view EV datasets`
3. Click **Create role** button


---

### Step 3.4: Update Consumer Trust Policy

1. Click on **EvDataConsumerRole** from list
2. Click **Trust relationships** tab
3. Click **Edit trust policy** button
4. Replace with same trust policy as Provider (change ACCOUNT-ID):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "cognito-idp.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    },
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    },
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::ACCOUNT-ID:root"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

5. Click **Update policy** button


---

## Step 4: Create Service Role for Backend Application

### Step 4.1: Create Service Role

1. Click **Create role** button
2. Select **AWS service** → **Lambda** (or **EC2** if deploying on EC2)
3. Click **Next**

![](/images/5-Workshops/lab2/task2/step4.1.png)

---

### Step 4.2: Add Both Policies to Service Role

1. Search and add both policies:
   - ✓ **EvDataProviderPolicy**
   - ✓ **EvDataConsumerPolicy**
2. Click **Next**


---

### Step 4.3: Name Service Role

1. In **Role name**, enter: `EvDataMarketplaceServiceRole`
2. In **Description**, enter: `Service role for EV marketplace backend application for S3 and Cognito access`
3. Click **Create role** button


---

## Summary

You have successfully created three IAM roles:

| Role Name | Policy Attached | Purpose |
|-----------|-----------------|---------|
| **EvDataProviderRole** | EvDataProviderPolicy | For data providers uploading datasets |
| **EvDataConsumerRole** | EvDataConsumerPolicy | For data consumers downloading datasets |
| **EvDataMarketplaceServiceRole** | Both policies | For backend application service |

All roles have been configured with proper trust relationships allowing:
- ✅ Cognito service to assume them
- ✅ EC2/Lambda services to assume them
- ✅ Root account to assume them

**Next Task:** Create IAM Users and assign them to roles

