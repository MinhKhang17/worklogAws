---
title : "Deploy CloudFormation Template"
date : 2026-03-16 
weight : 1
chapter : false
pre : " <b> 5.2.1 </b> "
---


[AWS CloudFormation](https://aws.amazon.com/cloudformation/) lets you model, provision, and manage AWS and third-party resources by treating infrastructure as code. In this step, we will deploy a CloudFormation stack to provision a VPC, EC2 instance, and S3 bucket.

---

1.  **Download template file and create new stack**
    
    Download the following [CloudFormation template](https://ws-assets-prod-iad-r-cmh-8d6e9c21a4dec77d.s3.us-east-2.amazonaws.com/e26c223d-6107-4ca8-a3c1-d8da486d7ea2/rc-workstation.yaml).
    
    Then, log into your AWS account and open up the CloudFormation console.
    
    On the Cloudformation console, click **Create Stack** -> **With new resources (standard)**.

---

2.  **Upload template to CloudFormation console**
    
    Under **Specify Template**, select the **Upload a template file** option, and upload the file from step 1. Then click **Next**.
    
    ![CFN Upload Template](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-cfn-create-stack.png)

---

3.  **Specify stack details**
    
    Provide the **Stack name** that you want to use, or you may use **rc-workshop**.
    
    * *The Stack name can include letters (A-Z and a-z), numbers (0-9), and dashes (-).*
    
    Provide the following information in the **Parameters** section:
    
    * **Availability Zone**
        * Choose **one** Availability Zone to use for the VPC.
        * *Note: You may select any of the availability zones from the dropdown menu.*
    * **VPC CIDR**
        * CIDR block for the VPC.
        * Please enter the first two octets of the CIDR block. The template completes the rest of the block for the subnets.
        * *Note: You may leave the default option (10.5) for the CIDR block, however, please ensure this block is not already in use.*
    * **Endpoint Device IP Address**
        * Enter the public IP of the endpoint device that will be used to connect to the Windows Server instance. For example: '128.128.128.128'.
        * You can also enter 0.0.0.0 for any IP, but it is not recommended.
    * **Desktop Instance Size**
        * You may use any of the instance types from the drop-down menu to complete this workshop.
        * The largest G5 instance type will complete the job the fastest, yet it will cost the most $$.
    * **Jump box Instance Size**
        * *Note: A jump server, or jump box is a system on a network used to access and manage devices in a separate security zone.*
    
    Click **Next**.

---

4.  **Create stack**
    
    On the **Configure stack options** page, leave all the defaults as-is. Scroll to the bottom and click **Next**.
    
    Finally, review the stack details you entered in step 3.
    
    Check the box that says *"I acknowledge that AWS CloudFormation might create IAM resources"* and click **Submit**.
    
    The deployment should take about **3-5 minutes.**

---

5.  **Confirm Successful Deployment**
    
    The **Events** tab will now be displayed, providing the status of the stack creation. Click the refresh icon to update the screen to show the latest progress.
    
    If your instance/stack creation is successful, the following message will appear.
    
    ![Stack Create Complete](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-stack-complete.png)

⚠️ **Stack Failure**
Common reasons for stack creation failures are that the requested instance type is not currently available for provisioning or the account that is used lacks the ability to spin up GPU-enabled instances. Please consult your IT team and/or Amazon technical support for proper advisement.