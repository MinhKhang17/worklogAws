---
title : "Clean up"
date : 2026-03-25
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

Follow these steps to clean up the resources which you have built for this lab to avoid having to pay for unused resources.

1.  Navigate to [AWS S3 Console](https://s3.console.aws.amazon.com/s3/home) and delete the S3 bucket created for this lab (`ev-data-marketplace-datasets-xxxxx`).  
    You must delete all objects and folders inside the bucket (datasets, metadata, logs, backups) before deleting the bucket itself.

2.  Navigate to [IAM Console](https://console.aws.amazon.com/iam/) and delete the IAM Users created in this lab:
    - `provider-test-user`
    - `consumer-test-user`  
    Make sure to delete access keys before removing the users.

3.  In IAM Console, go to **Roles** and delete the following roles:
    - `EvDataProviderRole`
    - `EvDataConsumerRole`
    - `EvDataMarketplaceServiceRole`

4.  In IAM Console, go to **Policies** and delete the custom policies:
    - `EvDataProviderPolicy`
    - `EvDataConsumerPolicy`  
    (Detach policies from roles before deleting if required)

5.  Navigate to [Amazon Cognito Console](https://console.aws.amazon.com/cognito/) and delete the User Pool:
    - `ev-marketplace-user-pool`

6.  Inside Cognito (if still exists), delete:
    - User groups: `Admins`, `DataProviders`, `DataConsumers`
    - App client: `ev-marketplace-app-client`
    - Domain configuration (if created)

7.  Verify that all resources have been removed:
    - No S3 buckets
    - No IAM users / roles / policies
    - No Cognito User Pools

# Thank you!

I hope you learned something new today and got inspired.