
# **Before Hands-on Lab**

# ***WORK IN PROGRESS, NOT TO SHARE***

During this time we will set up the environment need it for the Hands-on Lab.


## **Content:** ##

- [Exercise 1: Set up Environment](#exercise-1-set-up-environment)
   - [Task 1: Resources](#task-1-resources)



## **Exercise 1: Set up Environment** ##
During this exercise you will be setting up your  environment for this lab in Azure Virtual Machine acting as Azure Defender Sensors.

First we will set up an online sensor connected to IoT Hub, in the second step we will set up an offline sensor.


### **Task 1: Resources** ###

1. In Azure Portal, create a new Resource Group, from the home Page, select **+ Create a Resource** in the search box type **Resource Group**, then select **Create**.

In the next window, select your subscription, assign a name to the resource group **adt4iot+SUFFIX**, select a location and click on **Review + Create**, once you passed the validation, click **create** again

 ![Resource Group](./images/rg-create.png 'Resource Group')



2. In your browser, navigate to the [Azure portal](https://portal.azure.com), select **+Create a resource** in the navigation pane, enter `virtual Network` into the **Search the Marketplace** box.

3. Select **Virtual Network** from the results, and then select **Create**.

 ![Virtual Network](./images/Create-VN.PNG 'Virtual Netowrk')


4. In **Create virtual network**, enter or select this information in the **Basics** tab:

      | Setting | Value |
      | ------- | ----- |
      | **Project details** |   |
      | Subscription | Select your subscription. |
      | Resource group | Select the resource group just created above|
      | **Instance details** |   |
      | Name | Enter **myVNetwork**. |
      | Region | Select **(US) East US**. |

 ![Virtual Network Basics](./images/Create-VN-Basics.PNG  'Virtual Netowrk Basic')
   

5. Select the **IP Addresses** tab, or select the **Next: IP Addresses** button at the bottom of the page.

6. In **IPv4 address space**, select the existing address space and change it to **10.1.0.0/16**.

7. Select **+ Add subnet**, then enter **MySubnet** for **Subnet name** and **10.1.0.0/24** for **Subnet address range**.

8. Select **Add**.

 ![Virtual Network Subnet](./images/Create-VN-Add-Subnet.PNG  'Virtual Netowrk Subnet')

  >[!NOTE] You can ignore the warning as we are not intending to peer virtual networks.

9. Select **Next: Security** button at the bottom of the page. Under **BastionHost**, select **Enable**.

     ![Bastion Security](./images/enable-bastion-security.png 'Bastion Security')

    
10. Enter this information for the **BastionHost**:

    | Setting            | Value                      |
    |--------------------|----------------------------|
    | Bastion name | Enter **myBastionHost** |
    | AzureBastionSubnet address space | Enter **10.1.1.0/24** |
    | Public IP Address | Select **Create new**. </br> For **Name**, enter **myBastionIP**. </br> Select **OK**. |

11. Select the **Review + create** tab or select the **Review + create** button.

12. Once you passed the validation select **Create**.


13. It will take a few minutes to deploy. At the end you should see the your resources deployed.

 ![Deploy VN](./images/Create-VN-Deployment.PNG 'Deploy VN')

### **Task 2: Virtual Machines** ###

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
    | Image | Select **Windows 10 Pro, Version 20H2 - Gen1** |
    | Azure Spot instance | Select **No** |
    | Size | **Standard_D4s_v3 - 4 vcpus, 16 GiB memory** |
    | **Administrator Account** | **Use the following Credentials** |
    | Username | **ADefenderlab** |
    | Password | **Learningmode123!** |
    | Confirm password | **Learningmode123!** |
    | **Inbound port rules** |    |
    | Public inbound ports | Select **None**. |

    
![Create VM](./images/Create-VM-Basic.PNG 'Create VM')

3. Select the **Networking** tab, or select **Next: Disks**, then **Next: Networking**.

4. In the Networking tab, select or enter:

    | Setting | Value |
    |-|-|
    | **Network interface** |  |
    | Virtual network | Select **myVNetwork**. |
    | Subnet | Select **mySubnet** |
    | Public IP | Select **None** |
    | NIC network security group | Select **Basic**|
    | Public inbound ports network | Select **None**. |



5. Select the **Review + create** tab, or select the blue **Review + create** button at the bottom of the page.

6. Review the settings, and then select **Create**.

7. It will take a few minutes to deploy. At the end you should see the your resources deployed.


    ![Create VM](./images/Create-VM-Deployment.PNG 'Create VM')

### **Task 3: Connect to Virtual Machine** ###

1. Navigate to the Azure Portal Home and select your newly created virtual machine.

2. Make sure you that you start your Virtual Machine and that the status is **Running**.


![Running VM](./images/VM-status-running.PNG 'Running VM')


>[!TIP]
> You will not be able to start the Bastion connection if the VM has not been started and is running. So give it a minute or two to finish updating and wait for the status to say **"Running"**.


3. In the VM menu bar, select **Connect**, then select **Bastion**.

![Bastion Connect](./images/Connect-VM-Bastion.PNG 'Bastion Connect')


4. In the **Connect** page, select the blue **Use Bastion** button.



5. In the **Bastion** page, enter the username and password for the virtual machine.

    | Field | Enter |
    |-------|-------|
    | **Username** | *ADefenderlab* |
    | **Password** | *Learningmode123!* |

![Bastion Connect](./images/Connect-VM-Bastion-Connect.PNG 'Bastion Connect')

6. Select **Connect**.



7. A new tab should open, and you should be connected to your virtual machine.

8. **Accept** the default settings.


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


5. Set up Storage Account, upload defender images **WE NEED TO CAPTURE THE STEPS HERE I FORGOT PROBABLY THIS SHOULD BE THE FIRST STEP ALSO IN THE HOL?**

6. Login back to the Virtual Machine, using RDP or Bastiion, open in the Vm download Storage Explorer, open **Microsoft Edge** and download the ['Storage Explorer'](https://azure.microsoft.com/en-us/features/storage-explorer/ 'Storage Explorer') clikc **Download**

7. Once the download is completed run the installation selecting **Install for me only (recommended)** option. Next click on **Iaccept the agreement**, and **Install**, you will ask a few additional **Next** optiosn before starting the installation.

8. Next you will login to your Azure account where you save the Defender Files.Once Storage explorer opens select **Subscription**

    ![Storage Explorer](./images/sa-subs-login.png 'Subscription')

9.Next, click on **Azure**, **Next**. At this point you will ask your credentials to **Sign in** to Azure. Once you are signed in, close the browser, in the Storage you you should see your subscription.

10. On the left panel, you should see **Storage Accounts** under your Subscription.

    ![Storage Explorer Container](./images/container.png 'Select Container')

11. Once you selected the container on the right side you should see the files, just select the files and clikc **Download**

   ![Storage Explorer](./images/download-files.png 'Subscription')

 
    

