---
title : "Create an IAM User"
date : 2026-03-25
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---

AWS services such as Athena require valid credentials when you access them, so that the service can verify whether you have the appropriate permissions to access its resources. The AWS Management Console requires a password, and you can also generate access keys to interact via the CLI or API. However, it is strongly recommended that you avoid using your root AWS account credentials for day-to-day access. Instead, use AWS Identity and Access Management (IAM) to create a dedicated IAM user, add it to a group with administrative permissions, or assign administrative access directly. You can then access AWS via a unique sign-in URL using the IAM user credentials.

If you have already registered for AWS but have not yet created an IAM user for yourself, you can do so through the IAM console. If you are not yet comfortable using the console, refer to the AWS Management Console documentation for an overview.

**Steps to create an IAM user and assign it to an Administrators group**

1.  Use your AWS account email address and password to log in as the root user at the IAM console: [https://console.aws.amazon.com/iam/](https://console.aws.amazon.com/iam/) Note: It is strongly recommended to minimize root user usage. Lock away the root credentials securely and only use them for tasks that specifically require root-level access.

---

1.  In the navigation pane of the console, select **Users**, then click **Create user**.
    
2.  For **User name**, enter `Administrator`.
    
3.  Check the box next to **AWS Management Console access**, select **Custom password**, and type a password in the text field. Optionally, enable **Require password reset** to prompt the user to change their password on first sign-in.
    
4.  Click **Next: Permissions**.
    
5.  On the **Set permissions** page, choose **Add user to group**.
    
6.  Click **Create group**.
    
7.  In the **Create group** dialog, under **Group name**, type `Administrators`.
    
8.  Under **Filter policies**, check the box for **AWS managed - job function**.
    
9.  In the policy list, check the box for **AdministratorAccess**, then click **Create group**.
    
10.  Back in the group list, select your newly created group. Click **Refresh** if needed to see it in the list.
     
11.  Click **Next: Tags** to attach optional metadata to the user using key-value pairs.
     
12.  Click **Next: Review** to confirm the group membership settings. When ready, click **Create user**.
     

---

You can repeat this process to create additional groups and users, and to grant your users access to the appropriate AWS resources.

To sign in as the new IAM user, sign out of the AWS console and navigate to the following URL, replacing your\_aws\_account\_id with your AWS account number without hyphens (for example, if your account number is 1234-5678-9012, use 123456789012):

[https://your\_aws\_account\_id.signin.aws.amazon.com/console/](https://your_aws_account_id.signin.aws.amazon.com/console/) 

Enter the IAM user name (not your email address) and the password you just created. After signing in, the navigation bar will display "your\_user\_name @ your\_aws\_account\_id".

If you prefer not to expose your AWS account ID in the sign-in URL, you can set up an account alias. From the IAM console, choose **Dashboard** in the navigation pane. Under **IAM users sign-in link**, click **Customize** and enter an alias such as your company name. Once configured, use the following URL to sign in:

[https://your\_account\_alias.signin.aws.amazon.com/console/](https://your_account_alias.signin.aws.amazon.com/console/) 

To confirm the sign-in link for IAM users associated with your account, open the IAM console and look under **IAM users sign-in link** on the Dashboard.


