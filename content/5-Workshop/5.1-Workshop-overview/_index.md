---
title : "Overview"
date : 2026-03-16 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---


## What You'll Build

First, we'll set up a RealityCapture virtual workstation on an Amazon EC2 G5 instance. A RealityCapture virtual workstation allows users the ability to create or provision a virtual machine with graphical capabilities with Amazon Web Services (AWS), eliminating the need to run RealityCapture workloads locally on a graphics-enabled desktop or laptop computer.

Then, we'll walk through each step of running photogrammetry in the cloud. From uploading the image dataset to Amazon S3, starting a new job on RealityCapture using PowerShell, and exporting the model & textures back to S3.

![RC Diagram](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-workshop-arch.png)

---

## What You'll Need

* **AWS Account** - This account will require:
    * Permissions to deploy EC2 instances using CloudFormation templates
    * Service quota (8 or more) to launch EC2 G Type instances
    * Minimum EC2 instance type: g4dn.2xlarge or g5.2xlarge

ℹ️ **Request Quota for Amazon EC2 G Type**
RealityCapture requires an Amazon EC2 graphics instance (G type). **You will most likely need to request a service quota increase for this workshop.**
In your AWS account, navigate to Service Quotas, then AWS Services, search and select Amazon Elastic Cloud Compute (EC2). Then search and select “Running On-Demand G and VT instances”. If your account has less than 8 vCPUs for this instance type, request a quota increase of 8 or more EC2 vCPUs.
**Quota service increases are reviewed by AWS teams and may take a few days to process.**

⚠️ **Cost**
Free-tier AWS accounts do not have quota for G type EC2 instances. For details on Amazon EC2 Pricing, please visit [Amazon EC2 pricing](https://aws.amazon.com/ec2/pricing/). **Running the entire workshop followed by cleanup should incur costs of ~$10-15 USD.**

*Note: Costs may vary depending upon the region in which you deploy the stack, which instance type/size you choose, and how much time you spend exploring RealityCapture features outside of the prescribed workshop steps. When you are not working on the EC2 instance, make sure to shut it down so you do not incur costs of the instance running.*

*After you stop the instance, you are no longer charged usage or data transfer fees for it. However, you will still be billed for associated resources, such as attached EBS volumes and associated Elastic IP addresses.*

✅ **Available Regions**
This workshop will only work in the following AWS Regions: **us-east-1, us-east-2, us-west-1, us-west-2, ca-central-1, eu-central-1, ap-northeast-1**.

---

## What You'll Learn

In this workshop, you will learn how to:

* Use NICE DCV remote display protocol (RDP) to run graphics-intensive applications remotely on EC2 instances through a virtual workstation
* Use PowerShell to create a textured mesh with RealityCapture and save mesh to S3
* Deploy an AWS CloudFormation template