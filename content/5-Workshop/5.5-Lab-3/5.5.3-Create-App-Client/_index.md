---
title : "5.5.3 - Create App Client & Test Authentication"
date : 2026-03-25
weight : 3
chapter : false
pre : " <b> 5.5.3. </b> "
---

## Step-by-Step Guide: Create App Client & Test Authentication

### Objective
Configure the app client for OAuth authentication flows and test user sign-up/sign-in functionality.

---

## Step 1: Configure App Client Settings

1. In your Cognito user pool `ev-marketplace-user-pool`
2. Click **App integration** on the left menu
3. Click **App clients** 
4. You should see the app client created earlier: `ev-marketplace-app-client`
5. Click on it to edit settings


---

## Step 2: Configure Authentication Flows

1. In **Authentication flows and security**, configure:
   - ✓ **ALLOW_ADMIN_USER_PASSWORD_AUTH** (for testing)
   - ✓ **ALLOW_CUSTOM_AUTH**
   - ✓ **ALLOW_USER_PASSWORD_AUTH** (for app login)
   - ✓ **ALLOW_USER_SRP_AUTH** (secure password auth)
   - ✓ **ALLOW_REFRESH_TOKEN_AUTH** (token refresh)

2. Click **Save** button


---

## Step 3: Configure App Client Advanced Settings

1. In **Advanced app client settings**, set:
   - **Token expiration (in hours):**
     - Access token: `1` hour
     - ID token: `1` hour
     - Refresh token: `30` days

2. Click **Save** button


---

## Step 4: Get App Client Credentials

1. In **App client overview** or **App client settings**:
   - Note the **Client ID**
   - Note the **Client Secret** (if displayed)
   - Note the **App domain** or **Cognito domain**

2. These will be needed for backend configuration


---

## Step 5: Configure OAuth Domain (Custom Domain)

### Step 5.1: Navigate to Domain Configuration

1. In **App integration** menu, click **Domain name**
2. You'll see if a domain is already configured
3. If not, click **Create custom domain** button


---

### Step 5.2: Create Domain

1. Enter a custom domain name: `ev-marketplace`
   - Note: Must be globally unique
2. The full domain will be: `ev-marketplace.auth.us-east-1.amazoncognito.com`
3. Click **Create domain** button


---

## Step 6: Test User Sign-Up

### Step 6.1: Navigate to User Testing

1. In your user pool, click **Users** on left menu
2. Click **Create user** button to add a test user manually, OR
3. Use Cognito Hosted UI to test self-service sign-up


---

### Step 6.2: Access Hosted UI

1. In **App integration** → **App clients**
2. Click **Hosted UI** link
3. This opens the Cognito-provided login interface
4. Click **Sign up** to create a new test user


---

### Step 6.3: Create Test Users

Create two test users:

**User 1 - Provider:**
- Username: `provider-test`
- Email: `provider@marketplace.local`
- Password: `TempPass123!@#`
- Custom attribute - business_type: `provider`
- Custom attribute - company_name: `EV Data Inc`

**User 2 - Consumer:**
- Username: `consumer-test`
- Email: `consumer@marketplace.local`
- Password: `TempPass123!@#`
- Custom attribute - business_type: `consumer`
- Custom attribute - company_name: `EV Analysis Ltd`


---

## Step 7: Assign Users to Groups

### Step 7.1: Assign Provider User to Group

1. Go to **Users** in your user pool
2. Click on **provider-test** user
3. Click **User groups** tab
4. Click **Add to group**
5. Select **DataProviders** group
6. Click **Add** button


---

### Step 7.2: Assign Consumer User to Group

1. Go back to **Users**
2. Click on **consumer-test** user
3. Click **User groups** tab
4. Click **Add to group**
5. Select **DataConsumers** group
6. Click **Add** button


---

## Step 8: Verify Group Assignments

1. Return to user profiles
2. Confirm `provider-test` is in **DataProviders** group
3. Confirm `consumer-test` is in **DataConsumers** group


---

## Step 9: Test Authentication Flow

### Step 9.1: Test Provider Login

1. Go to Hosted UI (from App clients)
2. Sign in with provider credentials:
   - Username: `provider-test`
   - Password: `TempPass123!@#`
3. Should successfully authenticate
4. Copy the authorization code or ID token


---

### Step 9.2: Test Consumer Login

1. Sign out
2. Sign in with consumer credentials:
   - Username: `consumer-test`
   - Password: `TempPass123!@#`
3. Should successfully authenticate
4. Note the token claims (should show groups)


---

## Step 10: Verify JWT Tokens

### Step 10.1: Decode ID Token

1. Go to [jwt.io](https://jwt.io)
2. Paste the ID token from authentication
3. Verify the token contains:
   - `iss` (issuer) - Cognito URL
   - `sub` (subject) - User ID
   - `cognito:groups` - Should show group membership
   - Custom attributes (`company_name`, `business_type`)


---

## Summary

You have successfully configured Cognito authentication with:
- App client configured for OAuth flows
- Authentication flows enabled
- Token expiration set appropriately
- Custom domain configured
- Test users created in both groups
- Group memberships verified
- JWT tokens validated with group claims

**Lab 3 Complete!** Your Cognito infrastructure is ready for backend integration.

---

## Information to Save for Lab 4:

- **User Pool ID:** `us-east-1_xxxxxxxxx`
- **Client ID:** `xxxxxxxxxxxxxxxxxxxx`
- **Client Secret:** (if applicable)
- **Cognito Domain:** `ev-marketplace.auth.us-east-1.amazoncognito.com`
- **Test Provider User:** `provider-test` / Group: `DataProviders`
- **Test Consumer User:** `consumer-test` / Group: `DataConsumers`

**Next:** Proceed to Lab 4 - Integration with Java Spring Boot backend

