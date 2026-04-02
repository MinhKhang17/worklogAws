---
title : "5.3.1 - Create S3 Bucket"
date : 2026-03-25
weight : 1
chapter : false
pre : " <b> 5.3.1. </b> "
---

## Step-by-Step Guide: Create S3 Bucket

### Objective
Create an S3 bucket that will serve as the central storage for all EV Data Marketplace datasets, metadata, and transaction logs.

---

## Step 1: Open AWS Management Console

1. Navigate to [AWS Management Console](https://aws.amazon.com/console/)
2. Sign in with your AWS account credentials
3. Ensure you are in the **us-east-1** region (shown in top-right corner)

![AWS Management Console home page](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113457.png)

---

## Step 2: Navigate to S3 Service

1. In the search bar at the top, type **S3**
2. Click on **S3** from the dropdown results
3. The S3 Dashboard will load (showing buckets list)

![S3 Dashboard showing buckets list](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113617.png)

---

## Step 3: Create a New Bucket

1. Click the **Create bucket** button (orange button)
2. You will be redirected to the bucket creation form

![Create bucket button highlighted](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113723.png)

---

## Step 4: Configure Bucket Name

1. In the **Bucket name** field, enter:
   ```
   ev-data-marketplace-datasets-<your-account-id>
   ```
   Example: `ev-data-marketplace-datasets-123456789012`
   
   > **Note:** S3 bucket names must be globally unique and follow these rules:
   > - 3-63 characters long
   > - Only lowercase letters, numbers, and hyphens
   > - Must not start or end with a hyphen
   > - No underscores or uppercase letters

2. **Region:** Verify it's set to **us-east-1**

![Bucket name configuration form](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113750.png)

---

## Step 5: Review Bucket Settings

1. Keep the following defaults:
   - **Copy settings from existing bucket:** Leave unchecked
   - **ACLs disabled (Recommended)** is selected

2. Leave other options as default for now

![Bucket settings with defaults](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113823.png)

---

## Step 6: Create the Bucket

1. Scroll down to the bottom of the form
2. Click the **Create bucket** button
3. You should see a success message: "Successfully created bucket 'ev-data-marketplace-datasets-xxxxx'"

![Success message after bucket creation](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113848.png)

---

## Step 7: Verify Bucket Creation

1. Return to the S3 dashboard
2. You should see your new bucket in the buckets list
3. Click on the bucket name to open it
4. The bucket is now ready for configuration

![Newly created bucket visible in S3 list](/worklogAws/images/5-Workshops/lab1/Screenshot%202026-04-02%20113907.png)

---



**Next Task:** Configure versioning and encryption
