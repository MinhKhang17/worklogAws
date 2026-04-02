---
title : "5.5.2 - Configure User Groups"
date : 2026-03-25
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

## Step-by-Step Guide: Configure Cognito User Groups

### Objective
Create user groups in Cognito to manage role-based permissions: DataProviders group and DataConsumers group for marketplace users.

---

## Background: User Groups

User groups allow you to:
- Organize users by role or function
- Attach IAM roles to groups
- Manage permissions at the group level
- Support role-based access control (RBAC)

---

## Step 1: Open User Groups Configuration

1. In AWS Cognito console, click on your user pool: `ev-marketplace-user-pool`
2. On the left menu, click **User groups**
3. You'll see an empty groups list
4. Click **Create group** button

![](/images/5-Workshops/lab3/task2/step1.png)

---

## Step 2: Create DataProviders Group

### Step 2.1: Configure Group Details

1. In **Group name**, enter: `DataProviders`
2. In **Description**, enter: `Group for data providers who can upload and manage datasets`
3. In **IAM role**, choose the role we created in Lab 2: `EvDataProviderRole`
4. In **Priority**, enter: `1` (lower number = higher priority)
5. Click **Create group** button

![](/images/5-Workshops/lab3/task2/step2.1.png)

---

### Step 2.2: Verify DataProviders Group Created

1. You should see the DataProviders group in the list
2. Status shows the IAM role attached


---

## Step 3: Create DataConsumers Group

### Step 3.1: Configure Consumer Group

1. Click **Create group** button again
2. In **Group name**, enter: `DataConsumers`
3. In **Description**, enter: `Group for data consumers who can download and view datasets`
4. In **IAM role**, choose: `EvDataConsumerRole`
5. In **Priority**, enter: `2`
6. Click **Create group** button

![](/images/5-Workshops/lab3/task2/step3.1.png)

---

### Step 3.2: Verify DataConsumers Group Created

1. Both groups now appear in the list:
   - ✓ DataProviders (Priority 1)
   - ✓ DataConsumers (Priority 2)


---

## Step 4: Create Admin Group (Optional but Recommended)

### Step 4.1: Create Admin Group

1. Click **Create group** button
2. In **Group name**, enter: `Admins`
3. In **Description**, enter: `Administrators who can manage users and moderate datasets`
4. In **IAM role**, choose: `EvDataMarketplaceServiceRole` (or create an admin-specific role)
5. In **Priority**, enter: `0` (highest priority)
6. Click **Create group** button

![](/images/5-Workshops/lab3/task2/step4.1.png)

---

## Step 5: Verify All Groups

1. Your user pool should now have three groups:
   - ✓ **Admins** (Priority 0 - Highest)
   - ✓ **DataProviders** (Priority 1)
   - ✓ **DataConsumers** (Priority 2 - Lowest)

2. Each group has an associated IAM role for service integration


---

## Step 6: Add Custom Attributes to Groups (In APP)

While Cognito doesn't directly store custom group attributes, your backend application can:
1. Query groups from Cognito
2. Store additional metadata in a database
3. Use this for marketplace-specific settings

---

## Summary

You have successfully configured user groups with:
- **DataProviders group** → Access to provider features
- **DataConsumers group** → Access to consumer features
- **Admins group** → Full administrative access
- **IAM roles attached** → Clear permission hierarchy
- **Priority levels set** → Defines permission order

These groups are now ready to have users assigned to them.

**Next Task:** Create and configure app client for OAuth flow

