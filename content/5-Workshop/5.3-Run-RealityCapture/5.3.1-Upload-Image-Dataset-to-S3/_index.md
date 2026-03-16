---
title : "Upload Image Dataset to S3"
date : 2026-03-16
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---


In this step, we will upload our image dataset to Amazon S3. This Drone Imagery dataset contains 482 images that were captured with a drone and ground control points with precise location information. It can be used to check out how georeferencing works using images or ground control points.

Visit the Capturing Reality website for more [sample datasets](https://www.capturingreality.com/sample-datasets).

---

1.  **Download and unzip image dataset**
    
    Download dataset from [here](https://www.capturingreality.com/download/files/GCP-Drone-Sample-Dataset) and unzip the folder.

---

2.  **Create input folder on S3**
    
    On the CloudFormation console, open the stack you created in the previous *Setup Workstation* section and go to the **Resources** tab.
    
    Scroll down until you find the resource named **S3 Bucket**, click on the Physical ID. This will open the S3 console on a new tab.
    
    Click **Create Folder**, name the folder **Images** and leave all other default settings.
    
    ![S3 Create Folder](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-s3-create-folder.png)

---

3.  **Upload image dataset to S3**
    
    Open the image dataset folder you downloaded in step 1, and find the images in *DroneImagery_GCP/orthoPhoto/Images*.
    
    On the S3 console, open the **images** folder, and click **Upload**.
    
    ![S3 Upload Images](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-s3-upload.png)
    
    Upload images to S3 by using the drag and drop functionality, or by selecting the **Add Files** button.
    
    ![S3 Final Upload](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-s3-upload-confirm.png)
    
    At the bottom of the screen, leave all default settings and click **Upload** (this step should take around 5 minutes).

---

4.  **Create assets folder**
    
    Go to the root directory of the S3 bucket and create a new folder called **assets**.

---

5.  **Upload Texture Projection Settings & PowerShell Script files to S3**
    
    Download & unzip the following files: [Assets](https://ws-assets-prod-iad-r-iad-ed304a55c2ca1aee.s3.us-east-1.amazonaws.com/e26c223d-6107-4ca8-a3c1-d8da486d7ea2/rc-assets.zip)
    
    In the S3 console, open the **assets** folder created in Step 4, and click **Upload**.
    
    Upload the rcStart, rcSave, and TextureReprojectionSettings files to the S3 **assets** folder.
    
    ✅ **Learn more about the asset files:**
    * **Texture Reprojection Settings:** This file enables you to project a texture from an already textured model onto another model within the same component created in RealityCapture. You can project a texture created on a high-detail model onto a highly simplified model for considerably shorter time, and this way get the sharpest texture possible.
    * **rcStart:** This script is responsible for downloading the image dataset from S3 onto the EC2 instance, activating the RealityCapture license, starting a new RealityCapture job with the given parameters.
    * **rcSave:** This script saves the output model and project files to S3.