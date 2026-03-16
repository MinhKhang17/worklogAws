---
title : "Save to S3"
date : 2026-03-16 
weight : 4
chapter : false
pre : " <b> 5.3.4 </b> "
---


In this step, we will use PowerShell to save the RC project and FBX model to S3.

---

1.  **Run rcSave script**
    
    On the PowerShell app, save the model & project to S3 by executing the **rcSave** script (remove brackets):
    
    ```powershell
    C:\\RealityCapture\\rcSave.ps1 s3://[ENTER S3 BUCKET NAME]/output
    ```
    
    Go to the AWS console and open your workshop S3 bucket.
    
    You should now see a new folder named **output**, with two sub-folders: **model** and **project**.

---

2.  **(Optional) Examine rcSave script**
    
    There are two commands in this PowerShell script, the first saves the model files to S3, and the second saves the project files to S3:
    
    ```powershell
    Write-Output "Uploading Models to S3" 
    & "C:\\Program Files\\Amazon\\AWSCLIV2\\aws.exe" s3 cp "c:\\RealityCapture\model" ($Args[0]+"/model") --recursive     
    ```
    
    ```powershell
    Write-Output "Uploading Project to S3" 
    & "C:\\Program Files\\Amazon\\AWSCLIV2\\aws.exe" s3 cp "c:\\RealityCapture\rcproject" ($Args[0] + "/project") --recursive   
    ```

---

✅ **Congratulations!**
You have completed all the steps of this workshop. Please proceed to the **Cleanup** section.