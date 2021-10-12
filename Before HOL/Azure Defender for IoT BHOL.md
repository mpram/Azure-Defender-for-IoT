
# **Before Hands-on Lab**



During this time, we will set up the environment that is required for the Hands-on Lab.


## **Content:** ##

- [Exercise 1: Azure Passes](#exercise-1-azure-passes)
- [Exercise 2: Set up Environment](#exercise-2-set-up-environment)
   - [Task 1: Resources](#task-1-resources)
   - [Task 2: Virtual Machine](#task-2-virtual-machine)
   - [Task 3: Connect to Virtual Machine](#task-3-connect-to-virtual-machine)
   - [Task 4: Enable Hyper-V](#task-4-enable-hyper-v)
   - [Task 5: Create a Storage Account](#task-5-create-a-storage-account)
   - [Task 6: Azure Sentinel](#task-6-Azure-Sentinel)


## **Exercise 1: Azure Passes** ##

Previous to this workshop, after registration, you will receive an Azure Pass to configure with your personal email account, this step will be coordinated with your instructors.

Go to this link: https://www.microsoftazurepass.com/

Click on **START**, make sure you set up this pass with a personal email or just create an outlook email account for this training. After you login and validate the account. You will ask to **Enter the Promo Code**, here you will copy the Azure Pass Code you receive by email and then click on **Claim Promo Code**.


Next, fill the form with your name, after a few minutes you should have a Subscription available to start setting up your servicces in the next exercises. 

To validate your subscription is active, go to Azure Portal: https://portal.azure.com/

Right in the home portal you should see the icon for **Subscriptions** click on it you sould see a new Subscription available, also the same subscription could be available in the **Recent Resources** list.

 ![New Subscription](./images/nre-subs.png 'New Subscription')


If you don't see your subscription, validate you are accessing the right directory. Go to the top right corner menu, select **Directories+Subscriptions** icon and **Switch** button to change and validate again.

  ![Directory](./images/azure-directory.png 'Directory')




## **Exercise 2: Set up Environment** ##

Once your Azure Pass is activated and you have a new subscription to work with we will move to this exercise to create a resource group for all the services we will use to build our architecture.


### **Task 1: Resources** ###

1. In Azure Portal, create a new Resource Group, from the home Page, select **+ Create a Resource** in the search box type **Resource Group**, then select **Create**.

In the next window, select your subscription, assign a name to the resource group **adt4iot+SUFFIX**, select a location and click on **Review + Create**, once you passed the validation, click **create** again

 ![Resource Group](./images/rg-create.png 'Resource Group')


### **Task 2: Virtual Machine** ###

1. On the upper-left side of the portal, select: **Create a resource** > **Compute** > **Virtual machine** >> **Create**

![Deploy VM](./images/Create-VM.PNG 'Deploy VM')

2. In **Create a virtual machine**, type or select the values in the **Basics** tab:

    | Setting | Value                                          |
    |-----------------------|----------------------------------|
    | **Project Details** |  |
    | Subscription | Select your Azure subscription |
    | Resource Group | Select Your Resource Group |
    | **Instance details** |  |
    | Virtual machine name | Enter **myofflinesensor** |
    | Region | Select **(US) East US** |
    | Availability Options | Select **No infrastructure redundancy required** |
    | Image | Select **Windows 10 Pro, Version 20H2 - Gen2** |
    | Azure Spot instance | Select **No** |
    | Size | **D4s_v3 - 4 vcpus, 16 GiB memory**, see image below |
    | **Administrator Account** | **Use the following Credentials** |
    | Username | **ADefenderlab** |
    | Password | **Learningmode123!** |
    | Confirm password | **Learningmode123!** |
    | **Inbound port rules** |    |
    | Public inbound ports | Select **3389**. |
     | **Licensing** |    |
    | I confirm I have an eligible Windows 10 license with multi-tenant hosting rights. | **Check the box**. |


3. In the Size section, select **See all Images**, look for the **D-Series v3** open that section, then you will find the right VM.

![Create VM size](./images/vm-size.png 'Create VM size')

4. Go to the **Management**, in the **Monitoring** section, select **Disable** for **Boot Diagnostics**

5. At the bottom click on **Review + Create**. Once the validation is complete, select **Create**
    
![Create VM](./images/Create-VM-Basic.PNG 'Create VM')

6. It will take a few minutes to deploy. At the end you should see your resources deployed.


    ![Create VM](./images/Create-VM-Deployment.PNG 'Create VM')

### **Task 3: Connect to Virtual Machine** ###

1. Navigate to the Azure Portal Home and select your newly created virtual machine.

2. Make sure that the Virtual Machine status is **Running**.


![Running VM](./images/VM-status-running.PNG 'Running VM')


>[!TIP]
> You will not be able to connect if your Virtual Machines is not in **Running** status. So give it a minute or two to finish updating.


3. In the VM menu, select **Connect**, then select **Bastion** or **RDP**.

![Bastion Connect](./images/Connect-VM-Bastion.PNG 'Bastion Connect')

4. If you select **Bastion** you will be ask to set it up in 3 steps, **Step 1** it is completed, for **Step 2**, click on **Create Subnet**, after step 2 is completed, **Step 3** will set up a public ip, scroll down and click on **Create Azure Bastion using defaults**

![Bastion Connect](./images/set-up-bastion.png 'Bastion Connect')

After a few minutes you will be able to login

In the **Bastion** page, click on **Use Bastion** then enter the username and password for the virtual machine.

    | Field | Enter |
    |-------|-------|
    | **Username** | *ADefenderlab* |
    | **Password** | *Learningmode123!* |

![Bastion Connect](./images/Connect-VM-Bastion-Connect.PNG 'Bastion Connect')

5. Select **Connect**.



6. A new tab should open, and you should be connected to your virtual machine.

7. **Accept** the default settings.


![Bastion Connect](./images/VM-Bastion-Settings.PNG 'Bastion Connect')


### **Task 4: Enable Hyper-V** ###
We are going to enable Hyper-V via PowerShell in the newly created VM.

1. Search for **PowerShell** and right click to select **Run as Administrator**.


    ![PowerShell](./images/PowerShell-Admin.PNG 'PowerShell')


2. Run the following command:

  ```powershell
  Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
  ```

  If the command couldn't be found, make sure you're running PowerShell as an **Administrator**.

3. When the installation has completed, reboot the VM by typing in **Y**.



     ![PowerShell](./images/Hyper-V-Enabled.PNG 'PowerShell')

4. Reconnect to the VM.

>[!NOTE]
> If you are not promoted to restart the VM within PowerShell. Please close the Bastion Host tab, and return to the Azure Portal, and select your VM. At this point you can either "restart your VM" and reconnect via Bastion. OR you can *STOP* the VM and *Start* the VM again.


5. Login back to the Virtual Machine, using RDP or Bastion, open **Microsoft Edge** and download the ['Storage Explorer'](https://azure.microsoft.com/en-us/features/storage-explorer/ 'Storage Explorer') click **Download**.

6. Once the download is completed run the installation selecting **Install for me only (recommended)** option. Next, click on **I accept the agreement**, and **Install**, you will ask a few additional questions, select **Next** each time, the installation will run for a few seconds.



## **Task 5: Create a Storage Account**


1. In Azure Portal, click on **+ Create a Resource**. In the marketplace look for **Storage Account**, then click create.

2. Fill the form:

    ***Basics Tab:***
    - **Subscriptions**: Select the subscription you are using for this workshop.
    - **Resource Group**: Select the resource group created for this workshop in previous step.
    - **Storage Account Name**: adfiles+Suffix.
    - **Region**: East US
    - **Redundancy**: Locally-redundant storage(LRS)

Then **Review + Create** after the validation is complete, click **Create**

  ![SA](./images/sa-create.png
 'SA Create')


3. Once the Storage account is created, click on it. Under **Data Storage** select **Containers**, then on the right side select **+ Container**.

4. A new window will open on the right, assign a name **acitvationfiles** and then click **Create**.

  ![SA container](./images/create-container.png
 'SA Container')




5. Login to the Windows virtual machine, in the search box enter Microsoft Storage Explorer 

  ![SA](./images/storage-explorerbol.png
 'SA Open app')

6. You will be prompt to login, use the personal email you are using to set up your Azure Pass for this training.

7.  Once you are login, go to the connect icon on the left bar, then select **Storage account or service**.



![SA](./images/connect-to-sa.png
 'SA Open app') 


9. In the next step select **Shared Access Signature URL(SAS)** and then **Next**

![SA](./images/sas-url.png
 'SA Open app') 


10. In the Enter Connection Info window, you wil assign a name to the connection **HOLFiles** and you will paste below the Blob SAS URL (service URL) you received by email previous to this training.

![SA](./images/sas-url-input.png
 'SA Open app') 


11. Once the storage account is connected you should select the container on the left side **attendeefiles** then **Labfiles** now in the right side you will see the two files you need to download locally. Select the files and click **Download**

![SA](./images/files-ready.png
 'SA Open app') 


 12. Once this download is complete, go to the Azure Portal select your Virtual Machine and click **Stop**. Now you are all set for your training session. 

 ![Stop VM](./images/stop-machine.png
 'Stop VM') 

## **Task 6: Azure Sentinel** ##


1.	Go to Azure Portal, in the top search box, type **Azure Sentinel**, then select it from the list.

 
 ![Sentinel search](./images/search-sentinel.png 'Sentinel search') 

 2.	Then, click **Create**, a new pop up window appears, select **+ Create a new workspace**
 
 ![Sentinel create](./images/create-sentinel.png 'Sentinel create') 

 3. In the window, fill the form with the following data:
 - **Subscription**: Select the subscription you are using for this training.
 - **Resource Group**: select the resource group you created previously.
 - **Name**: Mylogworkspace+SUFFIX
 - **Regions**: East US
 
 ![Sentinel Create workspace](./images/create-workspace.png 'Sentinel create workspace') 

 4. Click **Review and create**, after validation is completed, click **create**
