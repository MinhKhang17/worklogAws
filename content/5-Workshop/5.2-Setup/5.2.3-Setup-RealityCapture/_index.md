---
title : "Setup RealityCapture"
date : 2026-03-16 
weight : 3
chapter : false
pre : " <b> 5.2.3 </b> "
---


Now that we've connected to the EC2 instance and have access to our virtual desktop, we will finalize the workstation setup and activate [RealityCapture](https://www.capturingreality.com/realitycapture/). RealityCapture is a photogrammetry software application for Windows, which enables you to create ultra-realistic 3D models from a set of images and/or laser scans.

---

1.  **(Optional) Adjust display settings**
    
    From your virtual workstation, right-click on the desktop and select **Display settings** from the menu.
    
    Select your display, and scroll down to the **Scale and layout** section.
    
    From the drop-down menu, adjust the display to **150%** or **175%**, or whichever size is best for your monitor.

---

2.  **Disable Internet Explorer Enhanced Security Settings**
    
    Type *PowerShell* into the search bar and open the **Windows PowerShell** app.
    
    Copy/paste the following code into PowerShell, then hit **Enter**:
    
    ```powershell
    function Disable-IEESC {
    $AdminKey = "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}"
    $UserKey = "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A8-37EF-4b3f-8CFC-4F3A74704073}"
    Set-ItemProperty -Path $AdminKey -Name "IsInstalled" -Value 0
    Set-ItemProperty -Path $UserKey -Name "IsInstalled" -Value 0
    Stop-Process -Name Explorer
    Write-Host "IE Enhanced Security Configuration (ESC) has been disabled." -ForegroundColor Green }
    Disable-IEESC
    ```
    
    This will disable Internet Explorer Enhanced Security settings.

---

3.  **Install Epic Games Launcher**
    
    Before you can install and launch RealityCapture, you’ll need to download the Epic Games Launcher.
    
    Go to the *Downloads* folder and find the EpicInstaller file. Open the file and go through each step of the installation wizard. You may leave all the default options as-is. **Installation should take 1-2 minutes.**
    
    If you do not see the EpicInstaller file in the Downloads folder, open the Microsoft Edge web browser and visit the [RealityCapture](https://www.capturingreality.com/realitycapture/) website.
    
    Click the **Download now** button on the top-right of the screen, then on the next page, click **Download Launcher**.
    
    Open the downloaded file and go through each step of the installation wizard. You may leave all the default options as-is. **Installation should take 1-2 minutes.**

---

4.  **Install RealityCapture**
    
    Open the Epic Games Launcher. Sign in if you have an Epic Games account, or create one if you do not.
    
    The RealityCapture installation wizard may automatically appear on the screen. If so, complete the installation (leave all defaults as is) and proceed to the next step.
    
    If the RealityCapture installation wizard does not appear, go to the Unreal Engine section of the launcher, and select the RealityCapture tab. Then click **Install**.
    
    ![Epic Games Launcher](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-epic-launcher.png)
    
    Accept the RealityCapture End User License Agreement, then complete the installation wizard steps (leave all defaults as-is). You should now have a RealityCapture shortcut on your Desktop.

---

5.  **Launch application**
    
    If not done automatically, you may now open the RealityCapture application.
    
    ![RC Launch](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-welcome-screen.png)