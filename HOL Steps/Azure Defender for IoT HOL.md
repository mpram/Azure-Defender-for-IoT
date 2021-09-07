# Internet of Things - Azure Defender for IoT  HOL

# ***WORK IN PROGRESS, NOT TO SHARE***

1) Azure Digital Twins, theory, deck presented avialable at **pdf files** folder.

Before Starting this Lab make sure you complete the steps specified in **Azure Digital Twins BHOL.md** File.

## Architecture Diagram ## 


Diagram here



## **Content:** ##
- [Exercise #1: Enabling Defender](#Exercise-1-Enabling-Defender)
  - [Task 1: Enabling Azure Defender for IoT](#Task-1-Enabling-Azure-Defender-for-IoT)
  - [Task 2: Setting up sensors](#Task-2-Setting-up-sensors)
  - [Task 3 - Onboarding sensors](#Task-3-Onboarding-sensors)
- [Exercise #2: Setting up your offline sensor](Exercise-2-Setting-up-your-offline-sensor)
  - [Task 1: Set up Virtual Machine](#Task-1-Set-up-Virtual-Machine)
  - [Task 2: Collect Information](#Task-2-Collect-Information)
  - [Task 3: Configure Azure Defender](#Task-3-Configure-Azure-Defender)
- [Exercise 3: Enabling system settings](#exercise-1-enabling-setting-settings)
   - [Task 1: System Properties](#task-1-System-properties)
  - [Task 2: Pcap Files](#task-2-Pcap-Files)
- [Exercise 4: Clean Up](#Exercise-4-Clean-Up)
  -[Task-1-Delete resources](#Task-1-Delete-resources) 

  


## **Exercise #1: Enabling Defender**

### **Task 1: Enabling Azure Defender for IoT:**

[In Azure Portal](#https://ms.portal.azure.com/) open **Security Center**, on the left panel under **Cloud Security** select **Azure Defender**

  ![Security Center](./images/security-center.png 'Security Center')

Next, select **IoT Security** under **Advanced Protection** section as shown below:

   ![IoT security Access](./images/iot-security.png 'IoT security Access')

Next in the **Getting Started** section, select **Oboard Subscription**


Before selecting your subscription make sure you select the option to **+ Start with Trial** as shown below:

   ![Trial Selection](./images/trial-selection.png 'Trial Selection')

Then, select your subscription and keep the devices selection to 1000, that is the minimum amout of devices configuration. These devices represents all those equipments/sensors connected to your network, this configuration allows you for a 30 days trial for free. Select **Evaluate** to continue.



### **Task 2: Setting up sensors:**



 2. After creation go to the resource group you just created, in the Overview panel, you will see at the top **+ Create**, click there and type **IoT Hub** in the search box, then clikc **Create**.

 3. In the next screen you will ask to fill the **Basics** tab

 - **Subscription**: Select the Subscription you are woking on.
 - **Resource Group**: Should be the resource group created in previous step.
 - **IoT Hub Name**: adt4iothub+SUFFIX
 - **Region**: East US


  ![IoT Hub Create](./images/iot-hub-create.png 'IoT Hub Create')
 


 Next, click on **Management** tab and make sure it is selected **S1:Standard Tier** in the **Pricing and scale tier** section.

 Last, clikc **Review + create**, once validation is completed, click **Create**


### **Task 3 - Onboarding sensors** ###

For the hands-on lab we will wrok with two type of sensors, one offline and one online connectected to Azure. In the next steps we will create both of them.


1. Go back to Azure Defender for IoT to create the sensors. You can go back through **Security Center**, **Cloud Security**, **Defender** then in the right side, under **Advanced Protection**, click on **IoT Security**

2. In the **Getting Started** section, select **Sensor**, then pick the **10.3.1 (Stable) and above - Recommended** version, and click **Download**.

![Onboard sensor](./images/onboard-sensor.png 'Onboard Sensor')

Fill the contact info window and then wait for a few minutes to complete the download.

3. Next go to **Sites and Sensors** and click on **+ Onboard sensor**

![Onboard sensor](./images/sensor.png 'Onboard Sensor')




4.Assigned a name to the sensor **myofflinesensor**, select your subscription and make sure you toogle **Cloud Connected** once you disable this option the rest of the form below will dissapear. Click **Register**




5. In the next step, click on **Download activation file** the activation zip and click **Finish**

 ![Activation Offline sensor](./images/downaload-offline-activation.png 'ActivationOffline Sensor')

6. You should see your sensor onboarded, locally managed, in your list of sensors as shown below.

![Sensor Onboarded](./images/sensor-onboarded.png 'Sensor Oonboarded')

7. Now, we will create another sensor, in this case we will be the online sensor. Click on **+ Onboard sensor**, in the next screen input the following information:
  - **Sensor name**: myonlinesensor
  - **Subscription**: Select the subscription you are using for this lab.
  - **Cloud Connected**: Enabled
  - **Automatic Threat Intelligence Updates**: Enable
  
  **Site** Section
  - **Hub**: Select the IoT Hub created in previous step.
  - **Display Name**:AD4IoTHub

  
  ![Onboard Online Sensor](./images/onboard-online-sensor.png 'Onboard Online Sensor')
 
 8. Click **Register**
 9. In the next step **Download activation file** and click **Finish**
 10. At this point if you check again your **Sites and sensors** section you should see both sensors onboarded.

11. The files just downloaded we will upload it to the Storage account created in the section **Azure Defender for IoT BHOL**, this way we will be able to make them available to download in the Virtual Machine. Another option could be to download the files directly in the Virtual Machine if you are login in Azure Portal directly insite the VM. However, sometimes you will have policies on place not allowing this, so the storage account route will make this feasible.


12. To Upload the Files, go to the Storage Account you created before. Select the container and click **Upload** from your local Download folder select the files and upload them.
 

13. Login back to the Virtual Machine, open **Storage Explorer**. You will be ask to login to your Azure account where you just upload the files.

**Subscription**

  ![Storage Explorer](./images/sa-subs-login.png 'Subscription')

8. Next, click on **Azure**, **Next**. At this point you will ask your credentials to **Sign in** to Azure. Once you are signed in, close the browser, in the Storage you you should see your subscription.

9. On the left panel, you should see **Storage Accounts** under your Subscription.

    ![Storage Explorer Container](./images/container.png 'Select Container')

10. Once you selected the container on the right side you should see the files, just select the files and clikc **Download**

   ![Storage Explorer](./images/download-files.png 'Subscription')

 
   

## **Exercise #2: Setting up your offline sensor**

During this exercise we will set up the Virtual Machine created before with Azure Defender. 

### **Task 1: Set up Virtual Machine**

1. Connect to the Virtual machine created, using RDP or Bastion.

2.  Open HyperV, select **New** on the left side will open multiple options, select **Virtual Machine**

 ![Onboard Online Sensor](./images/hyperv-create-vm.png 'Onboard Online Sensor')

3. In the first tab, assign a name **ad4iotsensoroffline**, then click **Next**

4. The next tab **Specify Generation**, select **Generation 1**, click **Next** again.

5. Then change the memory to **2024MB**, **Next** again.

6. **Configure Network** tab, select in **Connection**, **Default Switch**, **Next** again.

7. **Connect Virtual Hard Disk** tab, only modify the **Size** to 80GB as shown below, click **Next**.

 ![Disk Size](./images/disk-size.png 'Disk Size')

8.  In the **Connect Virtual Hard Disk** section, select **Install operating system from a bootable CD/DVD-ROM** option, then click in **Image file .(iso):** browse to the Download folder where you have the iso file downloaded from the Storage Explorer. Clikc **Next** and then **Finish**

![Disk Size](./images/select-iso.png 'Disk Size')


9. Now you have the Virtual Machine available and Off. right click on the VM, select **Settings**

10. Select **Network Adapter** and click **Add**. The select **Default Switch**, **Apply** and **Ok**

![Network Adapter](./images/network-adapter.png 'Network Adapter')

12. Select **Processor** section in hte left panel, and assign **2** to **Number of virtual processors**, select **Apply** and **Ok**.

13. Back to the VM, right click to **Start**, then right click again to **Connect**

14. When you connect to the VM after a few minutes of running the system installation, you should see the following configuration next

 ![Connect to  Sensor](./images/connect-to-sensor.png 'Connect to Sensor')
### **Task 2: Collect Information**

Before setting up Azure Defender is important you take a prtscrn of the Virtual Machine IP so both can communicate to each other, we are going to use this info to set up Defender.


1. Login to the Windows Virtual Machine where you are hosting the Ubuntu VM with Defender.
2. In the search box next to the windows logo, type **cmd** this should open a command window, type **ipconfig**, take a prtscrn, we will use this parameters to configure defender

![Network Properties](./images/network-properties.png 'Netowrk Properties')

Keep this screen open or take a prtscrn.

We will map this values in the next Task.

  
 ### **Task 3: Configure Azure Defender**

During this task we will configure Azure Defender, 

1. Press **Enter** for English.

2. Select the third option (Office 4CPUs)and press **Enter**


  ![Setting up  Sensor](./images/setting-up-sensor-version.png 'Setting up Sensor')

</br>

3. You will be ask to fulfill some parameters, it is ***VERY IMPORTANT*** you pay attention to the previous task because you will use the network information you captured before, this is unique to each Virtual Machine. So the following is an **EXAMPLE** based on the prtscrn presented above.


- **configure hardware profile**: **Office**, then press enter. 
- **Configure network interface**, type **eth0**
- **Configure management network interface**: this is an example **172.25.224.2**, you will use the **Ipv4 Address** from the previous task **+1 or -1** NOT THE SAME. Click Enter to continue
- **Subnets mask**: **255.255.240.0** this will be the SAME as the **Subnet Mask** captured in previous task.
- **Configure DNS**: **8.8.8.8**
- **Configure default gateway IP Address**: This value will be the sam as **Default Gateway** captured in previous task, in this example will be 10.4.0.1
- **Configure input interface(s)**: **eth1**
- **Configure bridge interface**: Just press Enter
- Then type **Y** and click **Enter**.

Now the installation will run for 10-15minutes.

***Note: Once the installation is complete, you will be able to access Azure Defender Console, check if you can open a cmd window, ping the Ip Adrress  you enter in the step 'Configure management network interface'
If the request timeout, you will need to reconfigure this step again, for that review the IPs one more time and use the command below to start over:***

```powershell
sudo cyberx-xsense-network-reconfigure 
```

Below, a ***sample*** screen, your parameters will be different.

 ![Setting up  Sensor](./images/defender-config.png 'Setting up Sensor')

</br>

4. ***IMPORTANT STEP!!!*** Once the installation is complete, you will have the login information availabe in the screen **TAKE THE PRTSCRN!!** before continuing, press **Enter**. Now you will have the support account, again in the screen **TAKE THE PRTSCRN!!** press **Enter** to continue.

</br>


![Setting up  Sensor](./images/login-info.png 'Setting up Sensor')

5. Open a brower, type the IP you use for the this step above **Configure management network interface**: this example was **172.25.224.2**, you should be able to login to Azure Defender 


![Defender Login](./images/defender-login-page.png 'Defender Login')

</br>

6. Login with the credentials provided in step **4**
7. Next, you will be ask to activate the product, click **Upload**, then **Browse Files**, in your dowloads folder select the file you downloaded from the Storage Explorer, in this example **myofflinesensor.zip**

![Defender Login](./images/activation.png 'Defender Login')

8. Click **Aprove these terms and Conditions**, then **Activate**.

9. You will be prompted to select **SSL/TLS Certificates | Onboarding 1/2** for this lab will use the second option **Use a locally generated self signed certificate(..)**. Then click **I CONFIRM**, **Next**.

![Certificate selection](./images/Certificate.png 'Certificate selection')
 
 10. For this lab in the next step we will **Disable** the system wide validation. **Finish**

 11. Let's analyze together what information we already have available before moving forward.

## **Exercise 3: Enabling system settings**

### **Task 1: System Properties**

1. In your offline sensor you will find **System Settings** on the left side of the Azure Defender portal, click there as shown below.

  ![system settings](./images/defender-system-settings.png 'System settings')

2. Next, look for the icon **System Properties** on the right side. Click in the icon, you will see a pop up warning, select **Ok**.

3. In the new window on the left side, scroll down until you see **Pcaps**, click there. Now on the right side scroll all the way down and we will modify three parameters as shown below:
  - **player_max_amount=200**
  - **enabled=1**
  - **player.params=-M 5**


  ![system settings pcaps](./images/enabling-pcaps.png 'System settings Pcaps')

4. Click **Save** and then **Ok**

5. Continue in the System Properties window, scroll up and select **Horizon** on the left side select, scroll down and modify the followin parameter:
  - **ui.enabled=true**


  ![Horizon Enable UI](./images/horizon-ui-enabled.png 'Horizon enable ui')

6. Click **Save** and then **Ok**

7. In system Properties, look for **Global** and modify the following parameter:
  - **auto_discovery.enabled=1**


  ![Global Settings](./images/global-settings.png 'global settings')

8. Click on **Save** and then **OK**

9. At this point you should see the Pcap Player available:

  ![Pcap Player](./images/pcap-player.png 'Pcap player')


</br>
  
### **Task 2: Pcap Files**

In this exercise your instructor will share the SAS token with you to download Pcap files to analyze and explorer further based on different scenarios and industries. 


1. Go to your Virtual Machine acting like a sensor, open **Microsoft Azure Storage Explorer** on the left side panel select the connect icon, an screen will pop up **Connect to Azure Storage** then click on **Use a shared access signature (SAS) URI**, **Next**


  ![Pcap Files](./images/connect-to-container.png 'Pcap files')


2. In the next screen your instructor will share the SAS Token with the class to connect to the container and download the files needed. 


3. Once you are connected to the Container, select all the files and click **Download**. Now you have all the files available locally and you can upload them to Azure Defender.


4. Go back to AZure Defender, Click on **System Settings**, then **PCAP Player** now select **Upload**,
**Browse Files**, browse to the folder where you download the files in the previous step, select all the files and click **Open**. This operation will take a few minutes to upload all the files.

5. At this point you should see all the files uploaded.



    ![Pcap Files Uploaded](./images/pcap-files-uploaded.png 'Pcap files uploaded')

</br>

6. Click on **Play All**, in a few minutes you will receive a message saying all the files has been played. 


## **Exercise 4: Analyzing the Data**

### **Task 1: Devices Map**


### **Task 2: Device Inventory**

### **Task 3: Alerts**

### **Task 4: Event Timeline**

### **Task 5: Data Mining**

</br>

## **Exercise 5: Online Sensor**

### **Task 1: Create an Online sensor**

### **Task 2: Integrate with Sentinel**

### **Task 3: Alerts - Intelligent Thread.**





</br>

## **Exercise 6: Clean Up**

### **Task 1: Delete resources**

The Azure Passes will allow you to run the services for 90 days for training porpose. Although it is a best practice to delete all your resources after the training. 

Search for the Resource Group created for this training.

Select Delete resource group on the top right side.

Enter your-resource-group-name for **TYPE THE RESOURCE GROUP NAME** and select Delete. This operation will take a few minutes.

After that is done go to Azure defender for IoT and deactivate the subscription.
