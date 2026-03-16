---
title : "Connect to EC2 instance"
date : 2026-03-16
weight : 2
chapter : false
pre : " <b> 5.2.2 </b> "
---


Now that the stack is successfully deployed, let's connect to the EC2 instance using [NICE DCV](https://aws.amazon.com/hpc/dcv/) remote display protocol (RDP). NICE DCV is a high-performance remote display protocol that provides customers with a secure way to deliver remote desktops and application streaming from any cloud or data center to any device, over varying network conditions. With NICE DCV and Amazon EC2, customers can run graphics-intensive applications remotely on EC2 instances, and stream their user interface to simpler client machines, eliminating the need for expensive dedicated workstations.

⚠️ **Warning**
The following command line instructions on this page are written for Mac/Linux machines. On Windows, you may complete these steps using the Command shell or PowerShell, however you must reference the Windows documentation to find the equivalent commands.

---

1.  **Create key pair file**
    
    On the AWS console, use the search bar and type **Parameter Store**.
    
    ℹ️ **Note**
    You may also reach Parameter Store by going to the Systems Manager console. You can find **Parameter Store** in the left-side navigation menu under **Application Management**.
    
    Find the parameter named "/ec2/keypair/key-***********", click the name to open the parameter details page.
    
    In the **Value** field, select **Show** to reveal the RSA private key.
    
    Copy this value from "-----BEGIN RSA PRIVATE KEY-----" to "-----END RSA PRIVATE KEY-----".
    
    ![EC2 Parameter Details](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-keypair.png)
    
    Open your terminal and create a key-pair file by running the following command:
    
    ℹ️ **Note**
    You may give this file any name, but it must end in **.pem**
    
    ```bash
    touch reality-capture.pem
    ```
    
    Edit this file with the following command:
    
    ```bash
    nano reality-capture.pem
    ```
    
    Copy-paste the RSA private key from the AWS console to this file. Then, save this file with **Ctrl+O** --> **Enter**.
    
    Exit the nano editor with **Ctrl+X**.

---

2.  **Verify instance launch and copy IP addresses**
    
    On the AWS console, use the search bar and type **EC2**.
    
    In the EC2 console, under *Resources*, click the **Instances (running)** link. You should see the two instances created by CloudFormation: **rc-workshop-workstation-base-ec2** and **rc-workshop-jumpbox-ec2**.
    
    Depending on the speed of provisioning, your VM may briefly appear as *initializing*.
    
    When the VM is completed its provisioning, it will appear as *running* with all its checks **passed**.
    
    ![Instance Status Passed](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-instance-running.png)
    
    For the instance named **rc-workshop-workstation-base-ec2**, copy the private IP address by clicking the blue link under **Instance ID**, and on the *Instance summary* page, locate the **Private IPv4 Address**. Paste it somewhere safe as it will be used in the next step.
    
    ![Instance Public IP](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-private-ip.png)
    
    For the jump box instance named **rc-workshop-jumpbox-ec2**, copy the public IP address by clicking the blue link under **Instance ID**, and on the *Instance summary* page, locate the **Public IPv4 Address**. Paste it somewhere safe as it will be used in the next step.
    
    ✅ **Jump Box**
    A jump server, or jump box is a system on a network used to access and manage devices in a separate security zone.
    
    ![Instance Public IP](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/public-ip.jpeg)
    
    ℹ️ **Note**
    Depending on your AWS security settings, adding or editing of security groups may be required before connecting to the VM. Please consult your IT/Information Security team for proper advisement.

---

3.  **Establish SSH connection**
    
    Open your terminal. Navigate to the folder where your key pair (.pem) file is saved.
    
    Make sure your file permission is 400 by running the following command:
    
    ```bash
    chmod 400 reality-capture.pem
    ```
    
    Use the following SSH command to connect into the public jump box, while also opening port 8888 locally and mapping it to the remote port 8443 on the private instance:
    
    ```bash
    ssh -i reality-capture.pem -L 8888:[INSERT PRIVATE IP SAVED IN STEP 2]:8443 ec2-user@[INSERT PUBLIC JUMPBOX IP]
    ```
    
    *Note: When inserting the public and private IP addresses into the SSH command, remove the surrounding brackets.*
    
    Answer **yes** to the prompted question. You should now be connected to the instance and see the following image in your terminal window.
    
    ![Terminal Instance Connected](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-ssh-connected.png)

---

4.  **Connect to the EC2 Instance**
    
    In order to connect to the EC2 instance, we will be using the NICE DCV client application. Please follow the [NICE DCV installation guide](https://docs.aws.amazon.com/dcv/latest/userguide/client.html) for your computer.
    
    Once the NICE DCV client application is installed, open it, and enter **localhost:8888**. Then select **Connect**.
    
    If you receive the following prompt, select **Trust and Connect**.
    
    To find the username and password, go to the EC2 console, and click on the instance named **rc-workshop-workstation-base-ec2**.
    
    On the Instance summary page, find and select the **Connect** button on the top right of the screen.
    
    Select the **RDP Client** tab.
    
    ![RDP Connect](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-rdp-connect.png)
    
    Copy the username (Administrator) and enter it in the NICE DCV client login screen.
    
    Decrypt & copy password:
    
    * Under Password, click **Get password**, this will open a new screen.
    * Click **Upload private key file**, find and select the key pair file you created in step 1.
        * *You may ignore the "Key pair associated with this instance" filename.*
    * Click **Decrypt password**, then the decrypted password should appear. Copy and paste the password to the NICE DCV client to finish logging in.
    
    ℹ️ **Note**
    If you receive an error message from NICE DCV with a failure to connect to the instance, ensure that your computer has outbound access to the Public or Private IP Address on TCP Port 8443.
    
    If successful, a Microsoft Windows desktop will appear.
    
    ![RC Virtual Desktop](https://static.us-east-1.prod.workshops.aws/public/ad6e3d8e-34b4-4fb9-af41-c9fbe3055ac5/static/rc-desktop.png)