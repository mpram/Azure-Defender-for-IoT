
# **Before Hands-on Lab**

During this time, we will set up the environment that is required for the Hands-on Lab.


## **Content:** ##

- [Action A: Azure Passes](#action-a-azure-passes)
- [Action B: Set up Environment](#action-b-set-up-environment)
   - [Task 1: Resources](#task-1-resources)
   - [Task 2: Virtual Machine](#task-2-virtual-machine)
   - [Task 3: Connect to Virtual Machine](#task-3-connect-to-virtual-machine)
   - [Task 4: Enable Hyper-V](#task-4-enable-hyper-v)
   - [Task 5: Create a Storage Account](#task-5-create-a-storage-account)
   - [Task 6: Azure Sentinel](#task-6-Azure-Sentinel)

</br>

## **Action A: Azure Passes** ##

Prior to this workshop, after successful registration, you will receive an Azure Pass. You can activate this Azure Pass with your personal email account. This step will be coordinated with your instructors.

Go to this link: https://www.microsoftazurepass.com/

Click on **START**, make sure you set up this pass with a personal email or just create an outlook email account for this training. After you login and validate the account. You will ask to **Enter the Promo Code**, here you will copy the Azure Pass Code you receive by email and then click on **Claim Promo Code**.

Next, fill the form with your name, after a few minutes you should have a Subscription available to start setting up your servicces in the next exercises. 

To validate your subscription is active, go to Azure Portal: https://portal.azure.com/

Right in the home portal you should see the icon for **Subscriptions** click on it you sould see a new Subscription available, also the same subscription could be available in the **Recent Resources** list.

![NewAzureSubscription](./images/AAT01-01-nre-subs.png 'New Subscription')

</br>

If you don't see your subscription, validate you are accessing the right directory. Go to the top right corner menu, select **Directories+Subscriptions** icon and **Switch** button to change and validate again.

![Dir](./images/AAT01-02-azure-directory.png 'Directory')

</br>

## **Action B: Set up Environment** ##

Once your Azure Pass is activated and you have a new subscription to work with, you are ready to setup the environment you will use during the Microsoft Defender for IoT Hands-on-Lab. For the HOL, you will create one single resource group to host all the services that you will use during the lab.

</br>

### **Task 1: Resources** ###

1. In the Azure Portal, create a new Resource Group. From the home Page, select **+ Create a Resource**, in the search box type **Resource Group**, then select **Create**.

    In the next window, select your subscription, assign a name to the resource group **rg-md4iot+SUFFIX**, select a location near you and click on **Review + Create**. Once you passed the validation, click **create** again. Note, the resource group name needs to be unique within your subscription. That is why we suggest to add a suffix, for instance your initials followed by a number.

    ![RG Create](./images/ABT01-01-rg-create.png 'Create a Resource Group')

</br>

### **Task 2: Virtual Machine** ###

1. In the upper-left side of the Azure Portal, select: **Create a resource** > **Compute** > **Virtual machine** >> **Create**

    ![VM Resource](./images/ABT02-01-resource-create.png 'Create VM resource')

</br>

2. In **Create a virtual machine**, type or select the values in the **Basics** tab:

    | Setting | Value                                          |
    |-----------------------|----------------------------------|
    | **Project Details** |  |
    | Subscription | Select your Azure subscription |
    | Resource Group | Select your just created Resource Group |
    | **Instance details** |  |
    | Virtual machine name | Enter **vm-md4iot-host** |
    | Region | Select **(EUROPE) West Europe** or a region near your location |
    | Availability Options | Select **No infrastructure redundancy required** |
    | Image | Select **Windows 10 Pro, Version 20H2 - Gen2** |
    | Azure Spot instance | Select **No** |
    | Size | **D4s_v3 - 4 vcpus, 16 GiB memory**, see image below |
    | **Administrator Account** | **Use the following Credentials** |
    | Username | **MDefenderLab** |
    | Password | **Learningmode123!** |
    | Confirm password | **Learningmode123!** |
    | **Inbound port rules** |    |
    | Public inbound ports | Select **3389** |
    | **Licensing** |    |
    | I confirm I have an eligible Windows 10 license with multi-tenant hosting rights. | **Check the box**. |

    </br>

    ![VM size](./images/ABT02-02-vm-create.png 'Create a new Virtual Machine')

</br>

3. In the Size section, select **See all Images**, look for the **D-Series v3** open that section, then you will find the right VM.

    ![VM size](./images/ABT02-03-vm-size.png 'Select VM size')

</br>

4. Go to the **Management** tab. In the **Monitoring** section, select **Disable** for **Boot Diagnostics**.

5. At the bottom click on **Review + Create**. Once the validation is complete, click **Create**.
    
6. It will take a few minutes to deploy your VM. At the end you should an indication that your deployment is complete.

    ![VM Deploy](./images/ABT02-04-vm-deployed.png 'VM deployment complete')

</br>

### **Task 3: Connect to Virtual Machine** ###

1. Navigate to the Azure Portal Home and select your newly created virtual machine.

2. Make sure that the Virtual Machine status is **Running**.

    ![VM Running](./images/ABT03-01-vm-running.png 'VM Status Running')

    </br>

    > **TIP:** You will not be able to connect if your Virtual Machines is not in **Running** status. So give it a minute or two to finish updating.

     </br>

3. In the VM menu, select **Connect**, then select **RDP**.

    ![VM Connect](./images/ABT03-02-vm-connect.png 'Virtual Machine Connection options')

    </br>

    > **NOTE:** In this HOL you are using RDP to connect to your virtual machine. A more secure option is to use Bastion, however, there are subscription costs we have to take into account. Because your Azure pass only has a limited amount of credit, we want to make sure that you get the most out of it working with Microsoft Defender for IoT.
  
    In the **Connect** page, click on **Download RDP File** and click on **Open**.

    ![RDP Download](./images/ABT03-03-download-rdpfile.png 'Download RDP file')

  </br>

4. In the RDP login screen, enter the username and password for the virtual machine.

    | Field | Enter |
    |-------|-------|
    | **Username** | *MDefenderLab* |
    | **Password** | *Learningmode123!* |

    ![RDP Login](./images/ABT03-04-rdp-login.png 'RDP Login to VM')

</br>

5. Click **OK** to login to the virtual machine.

6. A new window should open which is the connection to your Virtual Machine.
 
7. **Accept** the default settings.

    ![Default Settings](./images/ABT03-05-vm-connected.png 'Accept privacy settings')

</br>

### **Task 4: Enable Hyper-V** ###
We are going to enable Hyper-V via PowerShell in the newly created VM. This allows us to create additional virtual machines inside this virtual machine (a.k.a nested Hyper-v). This is one of the reasons why the VM we created is a relatively large one.

1. Search for **PowerShell** and right click to select **Run as Administrator**.

    ![SearchPS](./images/ABT04-01-Start-Powershell.png 'Run PowerShell as Admin')

</br>

2. Run the following command in the PowerShell Window:

   ``` powershell
   Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
   ```

   If the command couldn't be found, make sure you're running PowerShell as **Administrator**.

3. When the installation has completed, reboot the VM by typing in **Y**.

    ![PowerShell](./images/ABT04-02-HyperV-Enabled.png 'Enable Hyper-V')

</br>

4. Reconnect to the VM.

    > **NOTE:** If you are not prompted to restart the VM within PowerShell, please close the RDP Connetion, return to the Azure Portal and select your VM. At this point you can either "restart your VM" and reconnect via RDP or you can *STOP* the VM and *Start* the VM again.


5. Login back to the Virtual Machine, using RDP, open **Microsoft Edge** and download the ['Storage Explorer'](https://azure.microsoft.com/en-us/features/storage-explorer/ 'Storage Explorer') click **Download now**.

    ![StorageExplorer](./images/ABT04-03-download-storage-explorer.png 'Downloading Azure Storage Explorer')

</br>

6. Once the download is completed run the installation selecting **Install for me only (recommended)** option. Next, click on **I accept the agreement**, and **Install**, you will ask a few additional questions, select **Next** each time, the installation will run for a few seconds.

</br>

## **Task 5: Create a Storage Account**

You will execute this task on your physical machine, not in the Virtual Machine you created in the previous steps.

1. In Azure Portal, click on **+ Create a Resource**. In the marketplace look for **Storage Account**, then click **create**.

2. Fill the form:

    ***Basics Tab:***
    - **Subscriptions**: Select the subscription you are using for this workshop.
    - **Resource Group**: Select the resource group created for this workshop in one of the previous steps.
    - **Storage Account Name**: mdfiles+Suffix.
    - **Region**: *(EUROPE) West Europe* or a region near your location
    - **Performance**: Standard
    - **Redundancy**: Locally-redundant storage(LRS)

    Then **Review + Create** after the validation is complete, click **Create**

    ![SA](./images/ABT05-01-sa-create.png 'Create Storage Account')

</br>

3. Once the Storage account is created, click on it. Under **Data Storage** select **Containers**, then on the right side select **+ Container**.

4. A new window will open on the right, assign a name **activationfiles** and then click **Create**.

    ![SA container](./images/ABT05-02-sa-create-container.png 'Add Container to Storage Account')

</br>

5. Login to the Windows Virtual Machine you created earlier with RDP. In the search box on the desktop enter **Microsoft Storage Explorer**. 

    ![SA](./images/ABT05-03-storage-explorer.png 'Find Azure Storage Explorer')

</br>

6. You will be prompt to login, use the personal email you are using to set up your Azure Pass for this training.

7.  Once you are login, go to the connect icon on the left bar, then select **Storage account or service**.

    ![SAResource](./images/ABT05-04-connect-to-sa.png 'Select Azure Storage Explorer Resource') 

</br>

9. In the next step select **Shared Access Signature URL(SAS)** and then **Next**

    ![SAConnectMethod](./images/ABT05-05-sas-url.png  'Select Azure Storage Explorer Connection Method') 

</br>

10. In the Enter Connection Info window, you wil assign a name to the connection **HOLFiles** and you will paste below the Blob SAS URL (service URL) you received by email prior to this training.

    ![SAConnectInfo](./images/ABT05-06-sas-url-input.png  'Enter Azure Storage Explorer Connection Info') 

</br>

11. Once the storage account is connected you should select the container on the left side **attendeefiles** then **Labfiles** now in the right side you will see the two files you need to download locally. Select the files and click **Download**

    ![SAOpenApp](./images/ABT05-07-files-ready.png  'SA Open app') 

</br>

12. When this download is complete, close your RDP connection.

13. On your physical machine, go to the Azure Portal, select your Virtual Machine and click **Stop**. Now you are all set for your training session. 

    ![StopVM](./images/ABT05-08-stop-vm.png 'Stop the VM') 

</br>

## **Task 6: Azure Sentinel** ##

You will execute this task on your physical machine, not in the Virtual Machine you should have stopped in the previous step.

1.	Go to Azure Portal, in the top search box, type **Microsoft Sentinel**, then select it from the list.
 
    ![SentinelSearch](./images/ABT06-01-search-sentinel.png 'Sentinel search') 

2.	Then, click **Create**, a new pop up window appears, select **+ Create a new workspace**
 
    ![SentinelCreate](./images/ABT06-02-create-sentinel.png 'Sentinel create') 

3. In the new window, fill the form with the following data:
    - **Subscription**: Select the subscription you are using for this training.
    - **Resource Group**: select the resource group you created previously.
    - **Name**: Mylogworkspace+SUFFIX
    - **Regions**: West Europe (or another region close to you).
 
     ![SentinelCreateWS](./images/ABT06-03-create-log-analytics-ws.png 'Sentinel create workspace') 

 4. Click **Review and create**, after validation is completed, click **create**

 You have completed all your pre-work tasks before attending the Hands-on Lab! Please make sure your Virtual Machine is **STOP** until the training date, otherwise you will consume your Azure Credit before the training. 
