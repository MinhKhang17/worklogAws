---
title : "5.5.1 - Create Cognito User Pool"
date : 2026-03-25
weight : 1
chapter : false
pre : " <b> 5.5.1. </b> "
---

## Step-by-Step Guide: Create Cognito User Pool

### Objective
Create an Amazon Cognito User Pool as the authentication service for the EV Data Marketplace, allowing users to sign up, sign in, and manage their accounts.

---

## Background: Cognito User Pools

Cognito User Pools provide:
- User sign-up and sign-in
- Account management
- Password reset and recovery
- Multi-factor authentication (optional)
- Social identity provider integration (optional)

---

## Step 1: Open Amazon Cognito Console

1. In AWS Management Console, search for **Cognito**
2. Click **Cognito** from results
3. You'll see the Cognito dashboard
4. Click **Create user pool** button

![](/images/5-Workshops/lab3/task1/step1.png)

---

## Step 2: Configure Sign-in Experience

1. You're on **Configure sign-in experience** page
2. In **Provider types**, keep **Cognito user pool** selected
3. In **Cognito user pool sign-in options**, select:
   - ✓ **Email**
   - ✓ **User name**
   - (Allow users to sign in with email or username)
4. Click **Next** button

![](/images/5-Workshops/lab3/task1/step2.png)

---

## Step 3: Configure Security Requirements

1. You're on **Configure security requirements** page
2. In **Password policy**, select **Custom** to define custom rules:
   - Minimum length: **12** characters
   - ✓ Require uppercase
   - ✓ Require lowercase
   - ✓ Require numbers
   - ✓ Require special characters (@, #, $, %, etc.)
3. In **Multi-factor authentication (MFA)**, select **No MFA** (optional for now, can add later)
4. In **Account recovery**, keep default settings
5. Click **Next** button


---

## Step 4: Configure Sign-up Experience

1. You're on **Configure sign-up experience** page
2. In **Self-service sign-up**, select **Enable self-registration**
   - This allows new users to create accounts
3. In **Attribute verification and user account confirmation**, select:
   - **Send email message** (verify email)
   - **Automatically confirm and sign users in** is unchecked
4. In **Required attributes**, keep defaults:
   - Email (required)
5. In **Custom attributes**, we'll add custom attributes for our marketplace:
   - Click **Add custom attribute** button
   - Attribute name: `company_name`
   - Attribute type: **String**
   - Maximum length: **256**
6. Click **Add custom attribute** again for:
   - Attribute name: `business_type`
   - Attribute type: **String**
   - Values: `provider` or `consumer`
7. Click **Next** button


---

## Step 5: Configure Message Delivery

1. You're on **Configure message delivery** page
2. In **Email provider**, select **Send email with Cognito**
   - Use this for testing/development
   - For production, consider using Amazon SES
3. In **Email address display name**, enter: `EV Marketplace`
4. Leave email address as default
5. Click **Next** button


---

## Step 6: Integrate Your App

1. You're on **Integrate your app** page
2. In **User pool name**, enter: `ev-marketplace-user-pool`
3. In **App client name**, enter: `ev-marketplace-app-client`
4. In **Client type**, keep **Web client** selected (for web/mobile apps)
5. Make sure these are checked:
   - ✓ **Require client secret** (for security)
   - ✓ **Allow user password auth** (for programmatic access)
6. In **Allowed sign-out URLs**, enter:
   - `http://localhost:8080/logout` (for testing)
   - `http://localhost:3000/logout` (for frontend)
7. Click **Next** button


---

## Step 7: Review and Create

1. You're on **Review and create** page
2. Review all settings:
   - User pool name ✓
   - Sign-in options ✓
   - Security settings ✓
   - Custom attributes ✓
   - App client ✓
3. Click **Create user pool** button


---

## Step 8: Verify User Pool Created

1. You should see: "User pool created successfully"
2. You'll see the User Pool ID (like: `us-east-1_abcDefGhIj`)
3. Save this ID - you'll need it for backend configuration
4. Go to the **App clients and analytics** section
5. Click on your app client name to see:
   - Client ID
   - Client secret (if enabled)
   - Callback URLs
   - These will be needed in Lab 4


---

## Step 9: Configure Email Settings (Optional but Recommended)

1. In left menu, click **App integration** → **App clients**
2. Click on your app client
3. Under **App client settings**, configure:
   - **Allowed OAuth scopes:**
     - ✓ email
     - ✓ openid
     - ✓ profile
   - **Callback URLs:**
     - `http://localhost:8080/auth/callback`
     - `https://yourdomain.com/auth/callback` (production)
4. Click **Save** button


---

## Summary

You have successfully created a Cognito User Pool with:
- ✅ Email and username sign-in options
- ✅ Strong password policy requirements
- ✅ Custom attributes (company_name, business_type)
- ✅ Self-service registration enabled
- ✅ Email verification configured
- ✅ App client configured for OAuth
- ✅ User Pool ID and Client ID generated

**Important Information to Save:**
- User Pool ID: `us-east-1_xxxxxxxxx`
- Client ID: `xxxxxxxxxxxxxxxxxxxx`
- Client secret: (if enabled)

**Next Task:** Configure user groups for role-based access control

