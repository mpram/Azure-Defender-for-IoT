
# **Before Hands-on Lab**



During this time we will set up the environment need it for the Hands-on Lab.


## **Content:** ##

- [Exercise 1: Azure Passess](#azure-passess)
- [Exercise 2: Set up Environment](#exercise-1-set-up-environment)
   - [Task 1: Resources](#task-1-resources)
   - [Task 2: Virtual Machine](#Task-2-Virtual-Machine)
   - [Task 3: Connect to Virtual Machine](#Task-3-Connect-to-Virtual-Machine)
   - [Task 4: Enable Hyper-V](#Task-4-Enable-Hyper-V])
   - [Task 5: Create an Storage Account](#task-5-create-an-storage-account)


## **Exercise 1: Azure Passess** ##

Previous to this workshop, after registration, you will receive an Azure Pass to configure with your personal email account, this step will be coordinated with your instructors.


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
    | Size | **Standard_D4s_v3 - 4 vcpus, 16 GiB memory** |
    | **Administrator Account** | **Use the following Credentials** |
    | Username | **ADefenderlab** |
    | Password | **Learningmode123!** |
    | Confirm password | **Learningmode123!** |
    | **Inbound port rules** |    |
    | Public inbound ports | Select **3389**. |
     | **Licensing** |    |
    | I confirm I have an eligible Windows 10 license with multi-tenant hosting rights. | **Check the box**. |


3. Go to the **Management**, in the **Monitoring** section, select **Disable** for **Boot Diagnostics**

4. At the bottom click on **Review + Create**. Once the validation is complete, select **Create**
    
![Create VM](./images/Create-VM-Basic.PNG 'Create VM')

5. It will take a few minutes to deploy. At the end you should see the your resources deployed.


    ![Create VM](./images/Create-VM-Deployment.PNG 'Create VM')

### **Task 3: Connect to Virtual Machine** ###

1. Navigate to the Azure Portal Home and select your newly created virtual machine.

2. Make sure that the Virtual Machine status is **Running**.


![Running VM](./images/VM-status-running.PNG 'Running VM')


>[!TIP]
> You will not be able to connect if your Virtual Machines is not in **Running** status. So give it a minute or two to finish updating.


3. In the VM menu, select **Connect**, then select **Bastion** or **RDP**.

![Bastion Connect](./images/Connect-VM-Bastion.PNG 'Bastion Connect')

4. In the **Bastion** page, click on **Use Bastion** then  enter the username and password for the virtual machine.

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

6. Once the download is completed run the installation selecting **Install for me only (recommended)** option. Next, click on **I accept the agreement**, and **Install**, you will ask a few additional questions, select **Next** each time, the the installation will run for a few seconds.



## **Task 5: Create an Storage Account**


1. In Azure Portal, click on **+ Create a Resurce**. In the marketplace look for **Storage Account**, then click create.

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




