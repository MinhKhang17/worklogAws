---
title : "Lab 1: Create S3 Bucket"
date : 2026-03-25
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

## Overview

In this lab, you will create and configure an Amazon S3 bucket to store datasets for the EV Data Marketplace. This bucket will serve as the central repository for all data files, metadata, and transaction logs.

## Objectives

1. Create an S3 bucket with proper naming conventions
2. Configure bucket versioning to track dataset changes
3. Set up folder structure for datasets, metadata, and logs
4. Enable server-side encryption for security
5. Configure public access block settings
6. Set bucket policies for IAM access control

## Prerequisites

- AWS Account with administrative access
- AWS Management Console access
- Basic understanding of S3 concepts

## Key Tasks

- Create bucket: `ev-data-marketplace-datasets-{account-id}`
- Enable versioning
- Create folders: `/datasets`, `/metadata`, `/logs`
- Configure encryption (SSE-S3)
- Set public access blocks
- Define bucket policies for IAM role access

## Expected Outcome

A secure, versioned S3 bucket ready to store marketplace datasets with proper access controls.