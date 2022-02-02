
# Microsoft Defender for IoT - Before Hands-on Lab

During this time, we will set up the environment that is required for the Hands-on Lab.

## Content:

- [Action A: Azure Passes](#action-a-azure-passes)
  - [Task 1: Activating your Azure Pass](#task-1-activating-your-azure-pass)
  - [Task 2: Validating your Azure Subscription](#task-2-validating-your-azure-subscription)
- [Action B: Set up Environment](#action-b-set-up-environment)
  - [Task 1: Resources](#task-1-resources)
  - [Task 2: Virtual Machine](#task-2-virtual-machine)
  - [Task 3: Connect to Virtual Machine](#task-3-connect-to-virtual-machine)
  - [Task 4: Enable Hyper-V](#task-4-enable-hyper-v)
<!--- NOTE: When using Bastion to remote into the VM, the following section is needed!!!
  - [Task 5: Create a Storage Account](#task-5-create-a-storage-account)
-->
  - [Task 6: Microsoft Sentinel](#task-6-Microsoft-Sentinel)

## Action A: Azure Passes

Prior to this workshop, after successful registration, you will receive an Azure Pass. You can activate this Azure Pass with your personal email account. This step will be coordinated with your instructors.

### Task 1: Activating your Azure Pass

1. Go [here to activate your Azure Pass](https://www.microsoftazurepass.com/ 'Navigate to the Azure Pass Activation Site').
1. Click on **START**. Make sure you set up this pass with a personal email or just create an outlook email account for this training.
1. After you login and validate the account, you will be asked to **Enter the Promo Code**. Here you will copy the Azure Pass Code you received by email and then click on **Claim Promo Code**.
1. Next, fill the form with your name. After a few minutes you should have a Subscription available to start setting up your services in the next exercises. 

### Task 2: Validating your Azure Subscription

1. To validate your subscription is active, go to the [Azure Portal](https://poral.azure.com/ 'Navigate to the Azure Portal').
1. In the Azure Portal, you should see the icon for **Subscriptions**.
1. Click on it. You sould see a new Subscription available, also the same subscription could be available in the **Recent Resources** list.

   ![NewAzureSubscription](./images/ActA-T02-nre-subs.png 'New Subscription')

   > NOTE: If you don't see your subscription, validate you are accessing the right directory. Go to the top right corner menu, select the **Directories+Subscriptions** icon and the **Switch** button to change the directory and validate again.

   ![Dir](./images/ActA-T02-azure-directory.png 'Directory')

## Action B: Set up Environment

Once your Azure Pass is activated and you have a new subscription to work with, you are ready to setup the environment you will use during the Microsoft Defender for IoT Hands-on-Lab. For the HOL, you will create one single resource group to host all the services that you will use during the lab.

### Task 1: Resources

1. In the Azure Portal, create a new Resource Group. From the home Page, select **+ Create a Resource**, in the search box type **Resource Group**, then select **Create**.
1. In the next window, select your subscription, assign a name to the resource group: **rg-md4iot+SUFFIX**, select a location near you and click on **Review + Create**.
1. Once you passed the validation, click **create**.

   > Note: the resource group name needs to be unique within your subscription. That is why we suggest to add a suffix, for instance your initials followed by a number.

   ![RG Create](./images/ActB-T01-rg-create.png 'Create a Resource Group')

### Task 2: Virtual Machine

1. In the upper-left side of the Azure Portal, select: **Create a resource** > **Compute** > **Virtual machine** >> **Create**

   ![VM Resource](./images/ActB-T02-resource-create.png 'Create VM resource')

1. In **Create a virtual machine**, type or select the values in the **Basics** tab:

   | Setting | Value                                          |
   |-----------------------|----------------------------------|
   | **Project Details** |  |
   | Subscription | Select your Azure subscription |
   | Resource Group | Select your just created Resource Group |
   | **Instance details** |  |
   | Virtual machine name | Enter **vm-md4iot-host** |
   | Region | Select **(EUROPE) West Europe** or a region near your location |
   | Availability Options | Select **No infrastructure redundancy required** |
   | Security type | Select **Standard** |
   | Image | Select **Windows 10 Pro, Version 20H2 - Gen2** |
   | Azure Spot instance | Leave the checkbox unchecked |
   | Size | **D4s_v3 - 4 vcpus, 16 GiB memory**, see image below |
   | **Administrator Account** | **Use the following Credentials** |
   | Username | **MDefenderLab** |
   | Password | **Learningmode123!** |
   | Confirm password | **Learningmode123!** |
   | **Inbound port rules** |    |
   | Public inbound ports | Select **Allow selected ports** |
   | Select inbound ports | **RDP (3389)** |
   | **Licensing** |    |
   | I confirm I have an eligible Windows 10 license with multi-tenant hosting rights. | **Check the box**. |

   ![VMCreate](./images/ActB-T02-vm-create.png 'Create a new Virtual Machine')

1. In the Size section, select **See all Images**, look for the **D-Series v3** open that section, then you will find the right VM.

   ![VMsize](./images/ActB-T02-vm-size.png 'Select VM size')

1. Go to the **Management** tab. In the **Monitoring** section, select **Disable** for **Boot Diagnostics**.

1. At the bottom click on **Review + Create**. Once the validation is complete, click **Create**.
    
1. It will take a few minutes to deploy your VM. At the end you should an indication that your deployment is complete.

   ![VM Deploy](./images/ActB-T02-vm-deployed.png 'VM deployment complete')

### Task 3: Connect to Virtual Machine

1. Navigate to the Azure Portal Home and select your newly created virtual machine.

1. Make sure that the Virtual Machine status is **Running**.

   ![VM Running](./images/ActB-T03-vm-running.png 'VM Status Running')

   > **TIP:** You will not be able to connect if your Virtual Machines is not in **Running** status. So give it a minute or two to finish updating.

1. In the VM menu, select **Connect**, then select **RDP**.

   ![VM Connect](./images/ActB-T03-vm-connect.png 'Virtual Machine Connection options')

   > **NOTE:** In this HOL you are using RDP to connect to your virtual machine. A more secure option is to use Bastion, however, there are subscription costs we have to take into account. Because your Azure pass only has a limited amount of credit, we want to make sure that you get the most out of it working with Microsoft Defender for IoT.
  
1. In the **Connect** page, click on **Download RDP File** and click on **Open**.

   ![RDP Download](./images/ActB-T03-download-rdpfile.png 'Download RDP file')

1. In the RDP login screen, enter the username and password for the virtual machine.

   | Field | Enter |
   |-------|-------|
   | **Username** | *MDefenderLab* |
   | **Password** | *Learningmode123!* |

   ![RDP Login](./images/ActB-T03-rdp-login.png 'RDP Login to VM')

1. Click **OK** to login to the virtual machine.

1. A new window should open which is the connection to your Virtual Machine.
 
1. **Accept** the default settings.

   ![Default Settings](./images/ActB-T03-vm-connected.png 'Accept privacy settings')

### Task 4: Enable Hyper-V
We are going to enable Hyper-V via PowerShell in the newly created VM. This allows us to create additional virtual machines inside this virtual machine (a.k.a nested Hyper-v). This is one of the reasons why the VM we created is a relatively large one.

1. Search for **PowerShell** and right click to select **Run as Administrator**.

   ![SearchPS](./images/ActB-T04-Start-Powershell.png 'Run PowerShell as Admin')

1. Run the following command in the PowerShell Window:

   ``` powershell
   Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
   ```

   > **NOTE:** If the command couldn't be found, make sure you're running PowerShell as **Administrator**.

1. When the installation has completed, reboot the VM by typing in **Y**.

   ![PowerShell](./images/ActB-T04-HyperV-Enabled.png 'Enable Hyper-V')

1. Reconnect to the VM.

   > **NOTE:** If you are not prompted to restart the VM within PowerShell, please close the RDP Connetion, return to the Azure Portal and select your VM. At this point you can either "restart your VM" and reconnect via RDP or you can *STOP* the VM and *Start* the VM again.

1. Login back to the Virtual Machine, using RDP, open **Microsoft Edge** and download the ['Storage Explorer'](https://azure.microsoft.com/features/storage-explorer/ 'Storage Explorer') click **Download now**.

   ![StorageExplorer](./images/ActB-T04-download-storage-explorer.png 'Downloading Azure Storage Explorer')

1. Once the download is completed run the installation selecting **Install for me only (recommended)** option. Next, click on **I accept the agreement**, and **Install**, you will ask a few additional questions, select **Next** each time, the installation will run for a few seconds.

<!--- NOTE: When using Bastion to remote into the VM, the following instructions are needed to copy activation files to the VM that hosts the offline sensor!!!!

## Task 5: Create a Storage Account

You will execute this task on your physical machine, not in the Virtual Machine you created in the previous steps.

1. In Azure Portal, click on **+ Create a Resource**. In the marketplace look for **Storage Account**, then click **Create**.

1. Fill the form:

   ***Basics Tab:***
   - **Subscriptions**: Select the subscription you are using for this workshop.
   - **Resource Group**: Select the resource group created for this workshop in one of the previous steps.
   - **Storage Account Name**: mdfiles+Suffix.
   - **Region**: *(EUROPE) West Europe* or a region near your location
   - **Performance**: Standard
   - **Redundancy**: Locally-redundant storage(LRS) <br> <br>

1. Click **Review + Create**. After validation is complete, click **Create**

   ![SA](./images/ActB-T05-sa-create.png 'Create Storage Account')

1. Once the Storage account is created, click on it. Under **Data Storage** select **Containers**, then on the right side select **+ Container**.

1. A new window will open on the right, assign a name **activationfiles** and then click **Create**.

   ![SA container](./images/ActB-T05-sa-create-container.png 'Add Container to Storage Account')

-->

1. On the Windows Virtual Machine you created earlier, in the search box on the desktop enter **Microsoft Azure Storage Explorer** if you don't have the Azure Storage Explorer already open. 

   ![SA](./images/ActB-T05-storage-explorer.png 'Find Azure Storage Explorer')

1. Go to the connect icon on the left bar, and select **Storage account or service**.

   ![SAResource](./images/ActB-T05-connect-to-sa.png 'Select Azure Storage Explorer Resource') 

1. In the next step select **Shared Access Signature URL(SAS)** and then **Next**

   ![SAConnectMethod](./images/ActB-T05-sas-url.png 'Select Azure Storage Explorer Connection Method') 

1. In the Enter Connection Info window, you wil assign a name to the connection **HOLFiles** and you will paste below the Blob SAS URL (service URL) you received by email in the confirmation email that you received after registering for this HOL. If you didn't receive any confirmation mail (with subject *Microsoft Defender for IoT/OT Hands-on Lab: you are registered!*), please check your spam folder or send us an email at iotacademy@microsoft.com.  

   ![SAConnectInfo](./images/ActB-T05-sas-url-input.png 'Enter Azure Storage Explorer Connection Info') 

1. Once the storage account is connected you should select the container on the left side **attendeefiles** then **Labfiles** now in the right side you will see the two files you need to download locally. Select the files and click **Download**

   ![SAOpenApp](./images/ActB-T05-files-ready.png 'SA Open app') 

1. When this download is complete, close your RDP connection.

1. On your physical machine, go to the Azure Portal, select your Virtual Machine and click **Stop**. Now you are all set for your training session. 

   ![StopVM](./images/ActB-T05-stop-vm.png 'Stop the VM') 

## Task 6: Microsoft Sentinel

You will execute this task on your physical machine, not in the Virtual Machine you should have stopped in the previous step.

1.	Go to Azure Portal, in the top search box, type **Microsoft Sentinel**, then select it from the list.
 
    ![SentinelSearch](./images/ActB-T06-search-sentinel.png 'Sentinel search') 

1.	Then, click **Create**, a new pop up window appears, select **+ Create a new workspace**
 
    ![SentinelCreate](./images/ActB-T06-create-sentinel.png 'Sentinel create') 

1. In the new window, fill the form with the following data:

    - **Subscription**: Select the subscription you are using for this training.
    - **Resource Group**: select the resource group you created previously.
    - **Name**: Mylogworkspace+SUFFIX
    - **Regions**: West Europe (or another region close to you).
 
    ![SentinelCreateWS](./images/ActB-T06-create-log-analytics-ws.png 'Sentinel create workspace') 

 1. Click **Review and create**, after validation is completed, click **create**

 You have completed all your pre-work tasks before attending the Hands-on Lab! Please make sure your Virtual Machine is **STOP** until the training date, otherwise you will consume your Azure Credit before the training. 
