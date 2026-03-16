---
title : "Start Job"
date : 2026-03-16 
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---


In this step, we will use PowerShell to start a RealityCapture job. This job will do the following steps: 1/ align image dataset, 2/ construct a high poly base model, 3/ texturize the model, 4/ simplify the mesh into a low poly version.

---

1.  **Verify AWS CLI**
    
    On your virtual workstation desktop, type *PowerShell* into the search bar and open the **Windows PowerShell** app.
    
    Verify that the AWS CLI is installed by running:
    
    ```powershell
    aws --version
    ```
    
    A file path to the install should appear as output. If so, skip to the next step. If not, following the instructions below to download the AWS CLI.
    
    Install AWS CLI by executing the following command:
    
    ```powershell
    msiexec.exe /i [https://awscli.amazonaws.com/AWSCLIV2.msi](https://awscli.amazonaws.com/AWSCLIV2.msi)
    ```
    
    Complete the installation wizard (leave all default options).

---

2.  **Setup PowerShell credentials**
    
    **INTERNAL**
    
    If using an Isengard account, go to the [AWS Console Access Dashboard](https://isengard.amazon.com/console-access). Open the temporary credentials menu for the Isengard account you are using for this workshop.
    
    Expand the *PowerShell* drop-down menu, and click **Copy Powershell**.
    
    ![Set Temporary Credentials](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-temp-creds.png)
    
    To set the temporary credentials, copy and paste the credentials into the PowerShell app on your virtual workstation, then hit **Enter**.
    
    **EXTERNAL**
    
    Follow [these instructions](https://docs.aws.amazon.com/powershell/latest/userguide/creds-idc-cli.html) to configure credentials for PowerShell to use IAM Identity Center & AWS CLI.

---

3.  **Create job folders**
    
    Navigate to the "C:/" directory with the following command:
    
    ```powershell
    cd ../..
    ```
    
    Create a new folder named RealityCapture:
    
    ```powershell
    New-Item -Path "C:\" -Name "RealityCapture" -ItemType Directory
    ```
    
    Create three sub-folders named "model", "s3-input-images", "rcproject":
    
    ```powershell
    New-Item -Path C:\RealityCapture\model,C:\RealityCapture\s3-input-images,C:\RealityCapture\rcproject -ItemType Directory
    ```

---

4.  **Download asset files**
    
    On the S3 console, go to the workshop S3 bucket and copy the S3 URI of the **assets** folder as shown in the image below:
    
    ![S3 Assets URI](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-assets-s3-uri.png)
    
    Download the PowerShell Scripts & Texture Settings from S3 to your workstation using the following command (remove brackets):
    
    ```powershell
    aws s3 sync "[ENTER S3 URI OF ASSETS FOLDER]" C:\RealityCapture
    ```

---

5.  **Run rcStart script**
    
    Similar to Step 4, copy the S3 URI of the **images** folder.
    
    ℹ️ **Running RealityCapture from PowerShell**
    In the command below, we are running the **rcStart.ps1** script file with four parameters: 1/ job name, 2/ S3 input bucket/folder, 3/ polygon target for simplify step, 4/ RealityCapture activation key.
    
    Start a new RC job by executing the **rcStart** script file (remove brackets when replacing content):
    
    ```powershell
    C:\\RealityCapture\\rcStart.ps1 DroneImagery [ENTER S3 URI OF IMAGES FOLDER] 1000000
    ```
    
    ⚠️ **Duration estimate (based on instance size)**
    * g5.2xlarge = ~18 minutes
    * g5.4xlarge = ~15 minutes
    * g5.8xlarge = ~12 minutes

---

6.  **(Optional) Examine PowerShell output**
    
    If you examine the PowerShell output, you will see logs of each step in the job process.
    
    ![PowerShell job start](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-powershell-start.png)
    
    ![PowerShell job complete](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-powershell-complete.png)

---

7.  **(Optional) Examine rcStart script**
    
    In the **rcStart.ps1** script file, examine the *Running RC* command on line 48 that combines the image alignment (-align), mesh construction (-calculateNormalModel), mesh simplification (-simplify), and texturing (-calculateTexture) steps all into one command:
    
    ```powershell
    Write-Output "Running RC..." 
    & "C:\Program Files\Capturing Reality\RealityCapture\RealityCapture.exe" -newScene -headless -set "appQuitOnError=true"  -set "appProcessAction=ExecuteProgram" -set "appProcessActionTime=0" -stdConsole -writeProgress "C:\RealityCapture\ProcessingProgress.txt" -addFolder "C:\RealityCapture\s3-input-images" -align -selectMaximalComponent -setReconstructionRegionAuto -calculateNormalModel -renameSelectedModel HighPoly -calculateTexture -simplify ${simp} -renameSelectedModel LowPoly -unwrap -reprojectTexture HighPoly LowPoly C:\RealityCapture\TextureReprojectionSettings.xml -selectModel LowPoly -selectMarginalTriangles -removeSelectedTriangles -selectModel LowPoly -exportModel LowPoly C:\RealityCapture\model\LowPolyModel.fbx -save C:\RealityCapture\rcproject\Project.rcproj -quit
    ```
    
    This illustrates the ability to stack commands into one combined sequence. For a full list of RealityCapture CLI commands, see the [Capturing Reality documentation](https://rchelp.capturingreality.com/en-US/tutorials/commandline.htm).