---
title : "5.3.2 - Configure Versioning & Encryption"
date : 2026-03-25
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---

## Step-by-Step Guide: Configure Bucket Versioning and Encryption

### Objective
Enable versioning to track dataset changes and configure server-side encryption to protect sensitive data.

---

## Part A: Enable Bucket Versioning

### Step 1: Access Bucket Properties

1. In the S3 dashboard, locate your bucket `ev-data-marketplace-datasets-xxxxx`
2. Click on the bucket name to open it
3. Click on the **Properties** tab at the top

![S3 bucket properties tab](/images/5-Workshops/lab1/step1.png)

---

### Step 2: Navigate to Versioning

1. Scroll down in the Properties tab
2. Find the **Bucket Versioning** section
3. Click **Edit** button

![Bucket Versioning section](/images/5-Workshops/lab1/step2.png)

---

### Step 3: Enable Versioning

1. Select **Enable** option
2. Click **Save changes** button
3. You will see: "Bucket versioning status has been updated"

![Enable versioning confirmation](/images/5-Workshops/lab1/step3.png)

---

### Step 4: Verify Versioning

1. Return to the bucket properties
2. Confirm **Versioning** status shows: **Enabled**
3. This allows you to recover previous versions of dataset files

![Versioning status enabled](/images/5-Workshops/lab1/step4.png)

---

## Part B: Configure Server-Side Encryption

### Step 5: Access Encryption Settings

1. In the **Properties** tab, scroll to find **Encryption** section
2. Click **Edit** button in the Encryption section

![Encryption section](/images/5-Workshops/lab1/step5.png)

---

### Step 6: Configure Encryption Type

1. Select **Server-side encryption with Amazon S3-managed keys (SSE-S3)**
   - This is the recommended default encryption method
   - No additional cost
   - Key is managed by AWS

2. Do NOT select **SSE-KMS** (requires additional KMS setup)

![Encryption type selection](/images/5-Workshops/lab1/step6.png)

---

### Step 7: Enable Default Encryption

1. Check the box: **Enable default encryption**
2. Encryption type: Ensure **SSE-S3** is selected
3. Click **Save changes** button

![Default encryption enabled](/images/5-Workshops/lab1/step7.png)

---

### Step 8: Verify Encryption

1. Return to bucket Properties
2. Confirm **Encryption** shows: **Enabled (SSE-S3)**
3. All objects uploaded will be encrypted by default

![Encryption status confirmed](/images/5-Workshops/lab1/step8.png)

---

## Part C: Enable Public Access Block (Security Best Practice)

### Step 9: Access Public Access Block

1. Stay in **Properties** tab
2. Scroll to find **Block Public Access** section
3. Click **Edit** button

![Block Public Access section](/images/5-Workshops/lab1/step9.png)

---

### Step 10: Configure Access Restrictions

1. Ensure ALL four options are **Enabled**:
   - Block public access to buckets and objects granted through new access control lists (ACLs)
   - Block public access to buckets and objects granted through any access control lists (ACLs)
   - Block public access to buckets and objects granted through new public bucket or access point policies
   - Block public access to buckets and objects granted through any public bucket or access point policies

2. Click **Save changes** button


---

### Step 11: Verify Security Settings

1. Confirm all blocking options show as **On**
2. Your bucket is now secure from unauthorized public access


---

## Summary

You have successfully configured your S3 bucket with:
- **Versioning Enabled:** Track and recover previous dataset versions
-  **Server-Side Encryption (SSE-S3):** Protect data at rest
-  **Public Access Blocked:** Prevent unauthorized access
-  **Security Best Practices Applied**

**Next Task:** Set up folder structure for organizing datasets
