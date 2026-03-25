---
title : "3.2 Create an EMR Studio and attach it to the EMR cluster"
date : 2026-03-25
weight : 2
chapter : false
pre : " <b> 5.5.2 </b> "
---

**A. Get your EMR cluster's VPC and Subnet ID**

1.  First let's go to the [EMR console](https://console.aws.amazon.com/emr/home)  and on the left pane, select **Clusters** if it's not selected yet. You should see 1 cluster pre-provisioned for you.
    
2.  Click the Cluster ID to get your cluster details. In the cluster details page scroll to the bottom, and in the _Network and security_ section, copy the **VPC ID** and **Subnet ID** associated with your cluster. You will need these to create your Studio
    

---

**B. Create the EMR Studio environment**

1.  Now let's create a Studio environment, which is based on Jupyter, to connect to the EMR Cluster and do interactive development. Click on the **Studios** option from the left panel and then click on **Create Studio** button.
    
    ![EMRStudioPage](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/EMRStudioPage.png)
    
2.  From the Create a Studio page, select **Custom setup** then Click on **Browse S3** button to select your bucket for the S3 location for storage, then select **EMR\_Iceberg\_Notebook\_Role** for the Service role.
    
    ![Create Studio Bucket/Role](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/studio_setting_custom.png)
    
3.  Scroll down to the **Networking and security** section and select the VPC ID and subnet ID of your EMR cluster from Step A.2. Then click on **Create Studio and Launch Workspace**. After a few seconds, a new browser tab should open and you should see a familiar Jupyter notebook environment. (If a new tab does not open, please check on your popup blocker)
    
    ![Create Studio Bucket/Role](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/CreateStudioNetworkSetup.png)
    
4.  Once you see the notebook interface, click on the **Compute** icon on the left panel. Select **EMR on EC2 cluster** as the Compute type, then **select your cluster** from the drop down. Click **Attach** at the bottom.
    
    ![Create Studio Bucket/Role](https://static.us-east-1.prod.workshops.aws/public/ebc00129-fa83-4c1d-931e-1f301fc04542/static/AttachCluster.png)
    

**Congratulations! You have completed the EMR Studio/Workspace setup, now it's time to explore Iceberg features on EMR.**

