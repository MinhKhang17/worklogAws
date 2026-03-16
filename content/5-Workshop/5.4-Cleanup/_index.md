---
title : "Clean up"
date : 2026-03-16
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---


⚠️ **Stop instances when not in use**
You can stop the EC2 instances to avoid incurring costs without deleting the entire stack. Simply go to the EC2 console, and choose **Stop instance** under the **Instance state** drop-down.
After you stop the instance, you are no longer charged usage or data transfer fees for it. However, you will still be billed for associated resources, such as attached EBS volumes and associated Elastic IP addresses.

---

**Follow these instructions to remove all AWS resources you created in this workshop.**

1.  **Delete stack: Part 1**
    
    On the AWS console, go to **CloudFormation** and open the **Stacks** page.
    
    Select the dial or click on the stack name, then click the **Delete** button. This will delete all resources except the S3 bucket.
    
    Once complete, you will see the following message: *Delete Failed: The following resource(s) failed to delete: [S3Bucket]*
    
    ![RC Stack Delete Failed](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-delete-failed.png)

---

2.  **Delete stack: Part 2**
    
    (Optional) Before completing this step, you may download the contents of the workshop S3 bucket to save your work.
    
    On the AWS console, go to **S3** and open the workshop bucket.
    
    Delete each sub-folder: select the checkbox next to all three folder names, then click **Delete**. Follow the instructions on-screen to confirm the deletion.
    
    Go back to the **CloudFormation** console, open the workshop stack. Then once again, click **Delete** to finalize the stack deletion.
    
    You should see the final success message:
    
    ![RC Stack Delete Success](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-delete-complete.png)

---

✅ **Workshop Complete**