---
title : "5.4.1 - Create IAM Policies"
date : 2026-03-25
weight : 1
chapter : false
pre : " <b> 5.4.1. </b> "
---

## Step-by-Step Guide: Create IAM Policies

### Objective
Create custom IAM policies that define specific permissions for data providers and data consumers to interact with S3 bucket and marketplace resources.

---

## Background: Policy-Based Access Control

IAM policies are JSON documents that define what actions users/roles can perform on specific AWS resources. We will create two main policies:
- **EvDataProviderPolicy** → Upload and manage datasets
- **EvDataConsumerPolicy** → Download and view datasets

---

## Step 1: Open AWS IAM Console

1. In AWS Management Console, search for **IAM**
2. Click on **IAM** from results
3. On the left menu, click **Policies** under "Access management"

![](/worklogAws/images/5-Workshops/lab2/task1/step1.png)

---

## Step 2: Create Data Provider Policy

### Step 2.1: Start Creating Policy

1. Click **Create policy** button
2. Choose **JSON** tab (to enter raw policy document)
3. You'll see a text editor for the policy JSON

![](/worklogAws/images/5-Workshops/lab2/task1/step2.png)

---

### Step 2.2: Enter Provider Policy JSON

Delete the default content and paste this policy:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ListBuckets",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*"
        },
        {
            "Sid": "UploadDatasets",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:PutObjectAcl",
                "s3:GetObject"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*/datasets/*"
        },
        {
            "Sid": "ManageMetadata",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*/metadata/*"
        },
        {
            "Sid": "WriteTransactionLogs",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*/logs/transaction-logs/*"
        }
    ]
}
```

> **Note:** Replace `ev-data-marketplace-datasets-*` with your actual bucket name


---

### Step 2.3: Review and Name the Policy

1. Click **Next: Tags** button (or skip tags)
2. Click **Next: Review** button
3. In the **Policy name** field, enter: `EvDataProviderPolicy`
4. In **Description**, enter: `Policy for data providers to upload and manage datasets`
5. Click **Create policy** button


---

### Step 2.4: Verify Provider Policy Created

1. You should see success message: "The policy EvDataProviderPolicy has been created"
2. The policy is now available for assignment to users/roles


---

## Step 3: Create Data Consumer Policy

### Step 3.1: Start Creating Consumer Policy

1. Click **Create policy** button again
2. Choose **JSON** tab
3. Delete default content

![](/worklogAws/images/5-Workshops/lab2/task1/step3.png)

---

### Step 3.2: Enter Consumer Policy JSON

Paste this policy:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ListBuckets",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*"
        },
        {
            "Sid": "DownloadDatasets",
            "Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*/datasets/*"
        },
        {
            "Sid": "ViewMetadata",
            "Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*/metadata/dataset-descriptions/*"
        },
        {
            "Sid": "WriteAccessLogs",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject"
            ],
            "Resource": "arn:aws:s3:::ev-data-marketplace-datasets-*/logs/access-logs/*"
        }
    ]
}
```


---

### Step 3.3: Review and Name Consumer Policy

1. Click **Next: Tags** (skip if not needed)
2. Click **Next: Review**
3. In **Policy name** field, enter: `EvDataConsumerPolicy`
4. In **Description**, enter: `Policy for data consumers to download and view datasets`
5. Click **Create policy** button


---

### Step 3.4: Verify Consumer Policy Created

1. Success message: "The policy EvDataConsumerPolicy has been created"
2. Both policies are now ready for use


---

## Summary

You have successfully created two IAM policies:

| Policy Name | Purpose | Permissions |
|-------------|---------|------------|
| **EvDataProviderPolicy** | Data providers upload and manage datasets | Upload, Edit, Delete (datasets/metadata) |
| **EvDataConsumerPolicy** | Data consumers download datasets | Read-only access (datasets/metadata) |

Both policies follow the **principle of least privilege** - users only get the minimum permissions they need.

**Next Task:** Create IAM Roles and assign these policies to roles

