---
title : "Lab 3: Create Cognito User Pool"
date : 2026-03-16 
weight : 5 
chapter : false
pre : " <b> 5.5. </b> "
---

## Overview

In this lab, you will set up Amazon Cognito User Pool for authentication and authorization of EV Data Marketplace users. Cognito provides a secure, scalable way to manage user identities and implement single sign-on (SSO).

## Objectives

1. Create a Cognito User Pool for authentication
2. Configure user sign-up and sign-in flows
3. Set up password policies and MFA (optional)
4. Create user groups for role-based access control
5. Configure Cognito app client for backend integration
6. Set up user attributes for provider/consumer profiles

## Prerequisites

- Completed Lab 1 (S3 bucket created)
- Completed Lab 2 (IAM users and roles created)
- Understanding of authentication concepts

## Key Tasks

- Create User Pool: `ev-marketplace-user-pool`
- Configure password policy (length, complexity)
- Enable email verification
- Create user groups: `DataProviders` and `DataConsumers`
- Create app client for backend application
- Configure custom attributes (company name, business license, etc.)
- Test user sign-up and sign-in flows

## Expected Outcome

A fully functional Cognito User Pool with configured user groups, custom attributes, and app client ready for backend integration.