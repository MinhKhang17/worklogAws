---
title : "Lab 2: Create IAM User"
date : 2026-03-25
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

## Overview

In this lab, you will create and configure IAM users and roles for the EV Data Marketplace with appropriate permissions for S3 access. IAM (Identity and Access Management) controls who can access which AWS resources and what actions they can perform.

## Objectives

1. Create IAM policies for data provider and data consumer roles
2. Create service role for backend application
3. Configure S3 bucket access policies
4. Set up permissions for upload/download operations
5. Create IAM users for testing and development
6. Set up access keys for programmatic access

## Prerequisites

- Completed Lab 1 (S3 bucket created)
- Understanding of IAM concepts (users, roles, policies)
- Access to AWS IAM console

## Key Tasks

- Create IAM policy: `EvDataProviderPolicy` (upload, list, describe objects)
- Create IAM policy: `EvDataConsumerPolicy` (download, list objects)
- Create IAM role: `EvDataMarketplaceServiceRole` (for backend)
- Create IAM users: `provider-user` and `consumer-user` for testing
- Generate access keys for programmatic access
- Assign policies to users and roles

## Expected Outcome

IAM users and roles configured with least-privilege policies allowing providers to upload data and consumers to download data from the S3 bucket.