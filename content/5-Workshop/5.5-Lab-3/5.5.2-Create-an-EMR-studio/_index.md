---
title : "3.2 Set up EMR Studio and connect it to the EMR cluster"
date : 2026-03-25
weight : 2
chapter : false
pre : " <b> 5.5.2 </b> "
---

**A. Gather the VPC and Subnet ID of your EMR cluster**

1.  Navigate to the [Amazon EMR Console](https://console.aws.amazon.com/emr/home). In the left navigation pane, under **EMR on EC2**, choose **Clusters**.

2.  Click the **Cluster ID** of your cluster to open its details page. On the cluster details page, go to the **Summary** tab and scroll down to the **Network and security** section. Copy both the **VPC ID** and **Subnet ID** — you will need these when creating the Studio.

---

**B. Create the EMR Studio and Workspace**

1.  In the left navigation pane, still under **EMR on EC2**, select **Studios**. Then click **Create Studio**.

    ![EMRStudioPage](/images/5-Workshops/5.5/5.5.2/1.png)
    ![EMRStudioPage2](/images/5-Workshops/5.5/5.5.2/2.png)

2.  On the **Create a Studio** page:
    - Select **Custom setup**.
    - Click **Browse S3** to choose your S3 bucket as the notebook storage location.
    - Under **Service role**, select **EMR\_Iceberg\_Notebook\_Role**.

    ![Create Studio Bucket/Role](/images/5-Workshops/5.5/5.5.2/3.png)

3.  Scroll down to the **Networking and security** section. Choose the **VPC ID** and **Subnet ID** you copied in Step A.2. Then click **Create Studio**.

    ![Create Studio Bucket/Role](/images/5-Workshops/5.5/5.5.2/4.png)
    ![Create Studio Bucket/Role2](/images/5-Workshops/5.5/5.5.2/5.png)   

4.  Once the Studio is created, click **Launch Studio** to open it in a new browser tab. You will be presented with the JupyterLab interface.

    > **Note:** If a new tab doesn't open automatically, check your browser's popup blocker and allow popups for the AWS Console domain.

5.  Inside the JupyterLab interface, click the **Cluster** icon (or **Compute** icon) in the left sidebar. Under **Compute type**, select **EMR on EC2 cluster**, then pick your cluster from the dropdown. Click **Attach** at the bottom to link the cluster to your workspace.

    ![Create Studio Bucket/Role](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/AttachCluster.png)


**Congratulations! The EMR Studio/Workspace setup is complete. It's time to explore Iceberg features on EMR.**


