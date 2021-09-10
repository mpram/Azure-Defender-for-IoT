# Internet of Things - Azure Defender for IoT  HOL

# ***WORK IN PROGRESS, NOT TO SHARE***

Before Starting this Lab make sure you complete the steps specified in **Azure Defender for IoT BHOL.md** File.

## Architecture Diagram ## 


During this workshop we will be focusing on setting up our Azure Defender sensors, for online alerts and also offline scenarios, you will learn  how to configure your environment and assess the results. This hands-on lab will be focus on Securing your facilities, this will cover brownfield and greenfield devices. The scenario below is one of many you would apply these lessons, other scenarios are Oil & Gas, Utility and Energy companies.

  ![Architecture](./images/architecture-diagram.png 'Architecture Diagram')


## **Content:** ##
- [Exercise #1: Enabling Defender](#Exercise-1-Enabling-Defender)
  - [Task 1: Enabling Azure Defender for IoT](#Task-1-Enabling-Azure-Defender-for-IoT)
  - [Task 2: Setting up sensors](#Task-2-Setting-up-sensors)
  - [Task 3 - Onboarding sensors](#Task-3-Onboarding-sensors)
- [Exercise #2: Setting up your offline sensor](Exercise-2-Setting-up-your-offline-sensor)
  - [Task 1: Set up your offline sensor](#Task-1-Set-up-your-offline-sensor)
  - [Task 2: Collect Information](#Task-2-Collect-Information)
  - [Task 3: Configure Azure Defender](#Task-3-Configure-Azure-Defender)
- [Exercise 3: Enabling system settings](#exercise-1-enabling-setting-settings)
   - [Task 1: System Properties](#task-1-System-properties)
  - [Task 2: Pcap Files](#task-2-Pcap-Files)
- [Exercise 4: Analyzing the Data](#Exercise-4-Analyzing-the-Data)
	- [Task 1: Devices Map](#Task-1-Devices-Map)
	- [Task 2: Alerts](#Task-2-Alerts)
  - [Task 3: Device Inventory](#Task-2-Device-Inventory)
	- [Task 4: Event Timeline](#Task-4-Event-Timeline)
	- [Task 5: Data Mining](#Task-5-Data-Mining)
- [Exercise 5: Online Sensor](#Exercise-5-Online-Sensor)
	- [Task 1: Create an Online sensor](#Task-1-Create-an-Online-sensor)
	- [Task 2: Integrate with Sentinel](#Task-2-Integrate-with-Sentinel)
	- [Task 3: Alerts - Intelligent Thread](#Task-3-Alerts-Intelligent-Thread)

- [Exercise 6: Clean Up](#Exercise-6-Clean-Up)
	- [Task 1: Delete resources](#Task-1-Delete-resources)


  


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




4. Assigned a name to the sensor **myofflinesensor**, select your subscription and make sure you toogle **Cloud Connected** once you disable this option the rest of the form below will dissapear. Click **Register**




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
  - **Display Name**: AD4IoTHub

  
  ![Onboard Online Sensor](./images/onboard-online-sensor.png 'Onboard Online Sensor')
 
 8. Click **Register**
 9. In the next step **Download activation file** and click **Finish**
 10. At this point if you check again your **Sites and sensors** section you should see both sensors onboarded.

11. The files just downloaded we will upload it to the Storage account created in the section **Azure Defender for IoT BHOL**, this way we will be able to make them available to download in the Virtual Machine. Another option could be to download the files directly in the Virtual Machine if you are login in Azure Portal directly inside the VM. However, sometimes you will have policies on place not allowing this, so the storage account route will make this feasible.


12. To Upload the Files, go to the Storage Account you created before. Select the container and click **Upload** from your local Download folder select the files and upload them.
 

13. Login back to the Virtual Machine, open **Storage Explorer**. You will be ask to login to your Azure account where you just upload the files. Then select 
**Subscription**.

  ![Storage Explorer](./images/sa-subs-login.png 'Subscription')

8. Next, click on **Azure**, **Next**. Now **Sign in** to Azure. Once you are signed in, close the browser, in the Storage explorer you you should see your subscription.

9. On the left panel, select **Storage Accounts** under your Subscription.

    ![Storage Explorer Container](./images/container.png 'Select Container')

10. Once you selected the container on the right side you should see the files, just select the files and click **Download**

   ![Storage Explorer](./images/download-files.png 'Subscription')

 
   

## **Exercise #2: Setting up your offline sensor**

During this exercise we will set up the Virtual Machine created before with Azure Defender acting as a sensor offline.

### **Task 1: Set up your Virtual Machine**

1. Connect to the Virtual machine created, using RDP or Bastion.



2. Right click on your sensor, under **Hyper-V Manager**, left side, and select **Virtual Switch Manager**


  ![Virtual Switch](./images/virtual-switch.png 'Virtual Switch')


3. A new window will pop up, select **New Virtual network switch**, then **Internal**, **Create virtual switch**. Assign a name **MySwitch**. Last **Aplly** and **Ok**

  ![Virtual Switch](./images/create-virtual-switch.png 'Virtual Switch')


4. Back in the HyperV, select **New** on the left side will open multiple options, select **Virtual Machine**

 ![Onboard Online Sensor](./images/hyperv-create-vm.png 'Onboard Online Sensor')

  - First tab, assign a name **ad4iotsensoroffline**, then click **Next**

  - **Specify Generation**, select **Generation 1**, click **Next** again.

  - Change the memory to **2024MB**, **Next**.

  - **Configure Network** tab, select in **Connection**, **Default Switch**, **Next**.

  - **Connect Virtual Hard Disk** tab, **Create a virtual hard disk** click **Next**.

 - **Installations Options**, select **Install an operating system from a bootable CD/DVD-ROM** then select **Image file (.iso)** and browse the Azure defender .iso file downloaded in previous steps. Last **Finish**


![Disk Size](./images/select-iso.png 'Disk Size')

5. Back to the VM, right click to **Start**, then right click again to **Connect**

6. When you connect to the VM after a few minutes of running the system installation, you should see the following screen

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


- **configure hardware profile**: **office**, then press enter. 
- **Configure network interface**, type **eth0**
- **Configure management network interface**: this is an example **172.25.224.2**, you will use the **Ipv4 Address** from the previous task **+1 or -1** NOT THE SAME. Click Enter to continue. ***Take a note of this IP you will need it later on***.
- **Subnets mask**: **255.255.240.0** this will be the SAME as the **Subnet Mask** captured in previous task.
- **Configure DNS**: **8.8.8.8**
- **Configure default gateway IP Address**: This value will be the same as **Default Gateway** captured in previous task, in this example will be 10.4.0.1
- **Configure input interface(s)**: **eth1**
- **Configure bridge interface**: Just press Enter
- Then type **Y** and click **Enter**.

Now the installation will run for 10-15minutes.

***Note: Once the installation is complete, you will be able to access Azure Defender Console, check if you can open a cmd window, ping the IP Address  you enter in the step 'Configure management network interface'
If the request timeout, you will need to reconfigure this step again, for that review the IPs one more time and use the command below to start over:***

```powershell
sudo cyberx-xsense-network-reconfigure 
```

Below, a ***sample*** screen, your parameters will be different.

 ![Setting up  Sensor](./images/defender-config.png 'Setting up Sensor')

</br>

4. ***IMPORTANT STEP!!!*** Once the installation is complete, you will have the login information availabe in the screen **TAKE THE PRTSCRN!!** before continuing, press **Enter**. Now you will have the support account, again in the screen **TAKE THE PRTSCRN!!** press **Enter** to continue. If you fail to capture the credentials, you will need to start over.

</br>


![Setting up  Sensor](./images/login-info.png 'Setting up Sensor')

5. Once the installation finished you will ask to login, enter the credentials from previous step. In this screen you can also validate the IP, you will use that IP in your browser.

</br>

***Note: At this stage your IPs should look similar to the example below, if you can't reach the portal validate the IPs. If you restarted your VM there is a chance your IPs changed so you will need to go back and reconfigure them, if that is the case use the command in step 3.***

</br>

![Defender IP](./images/validate-ip.png 'Defender IP')

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

5. Continue in the System Properties window, scroll up and select **Horizon** on the left side select, scroll down and modify the following parameter:
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


4. Go back to Azure Defender, Click on **System Settings**, then **PCAP Player** now select **Upload**,
**Browse Files**, browse to the folder where you download the files in the previous step, select all the files and click **Open**. This operation will take a few minutes to upload all the files.

5. At this point you should see all the files uploaded.



    ![Pcap Files Uploaded](./images/pcap-files-uploaded.png 'Pcap files uploaded')

</br>

6. Click on **Play All**, in a few minutes you will receive a message saying all the files has been played. 


## **Exercise 4: Analyzing the Data**

After Azude Defender learnt about your environment it will be able to share insights pretty fast.

### **Task 1: Devices Map**

Your first interaction with Devices map you will see a similar map like the below

   ![Pcap Files Uploaded](./images/devices-map.png 'Pcap files uploaded')
1. Use the four icon on the left to select **Layout by Purdue**. In this model you will see the different layers between Corporate IT and site opeartions.


2. Check your notifications available and you can take action at this point.

3. For each device right click to analyze properties, show events, reports and simulate attack vectors.


4. In the hamburguer menu on the left, click the highlights and select one of the **OT Protocols** i.e. **MODBUS** and click on **Filter**. Now your map will show those devices only


  ![Pcap Files Uploaded](./images/device-map-filtering.png'Pcap files uploaded')


5. Then filter your devices by **CIP** OT Protocol, at the bottom of your map you will see a PLC, where the Vendor is Rockwell Automation, has already 3 alerts activated. Right click on the device, **View Properties**. In this view you will be able to analyze the Backbone of your PLCs, take actions and analyze the Alerts.


  ![PLC](./images/plc.png 'PLC')

### **Task 2: Alerts**

1. Once you click Alerts in your PLC you will see a new window pop up showing three different types of alerts.
    - Operational(high Alert and lower alert)
    - Policy Violation

For each of these alerts you will be able to analyze the pcap file, export a report, analyze the timeline or mute the alert.

2. If we remove the device filter from the top of the screen, then click **Confirm** you will see 20 Alerts in process.


3. Apply **Custom Groups** to filter different scenarios, such as **Unclassified subnets** then **Confirm**


### **Task 3: Device Inventory**
1. In this view, filter all your devices by **Is Authorized**, True or False are possible values.

2. Organize your devices based on filters.

3. Export the list to a csv files.


### **Task 4: Event Timeline**

This vewi will allow you a Forensic analysis of your alerts.

1. Choose **Advanced Filers**, filter the timeline by **CIP**, let's analyze the alert timeline.


### **Task 5: Data Mining**

In this section you can create multiple custom reports.
As an example we will create a Report based on firmware updates versions.

1. Go To **+**, **New report**, in the categories section select **Modules and Firmware update versions**

2. Assign a name to your report. Then go to Filters, **add** and select **Firmware version(generic)**

  ![PLC](./images/dm-firmware.png 'PLC')

3. In the new field added **Firmware Version(GENERIC)** add **0.4.1**, then **Save**.

4. You can remove the filter to list all the firmware updates version in your list also.

5. Export you report(pdf, csv) for further actions. 


### **Task 6: Risk Assessment**

1. Go to the Risk assessment, run the assessment. During this task we will show you how to analyze the assessment. 

***IMPORTANT***, after completing this workshop you will have a period of two weeks to run the risk assessment in your evironment and schedule an appoitment with our Cybersecurity team to guide you through analysis, best practices and vulnerabilities in your facilities.

</br>

## **Exercise 5: Online Sensor**

To modfy our sensor to be an online sensor, we will use the same virtual machine but we will modify the activation file creating a new sensor in Azure Defender. 

### **Task 1: Create an Online sensor**

1. Go to Azure Portal, select **Security Center**, under **Cloud Security** click on **Azure Defender**. Look for **IoT Security** at the bottom of the right side.

2. In the new window, on the left panel you will find **Sites and sensors**. Click on **+ Onboard sensor**

3. Fill the form:
    - **Name**: myonlinesensor
    - **Subscription**: Select the Subscrition you are using for this workshop.
    - **Cloud Connected**: Enabled
    - **Automatic Threat Intelligence Updates (Preview)**: Enabled

    ***Site Section***
    - **Hub**: Select the hub created during **Before hands-on lab** section
    - **Name**: no needed.
    - **Tags**: blank.

  Then **Register**

4. In the next window, **Download activation file** and **Finish**

  ![Online sensor](./images/online-sensor.png 'Online Sensor')
5. Go to the resource group you are using for training, look for the storage account created in **Azure Defender for IoT BHOL** section, click on it. 

6. On the left side panel, select **Containers** under **Data Storage section**, click on **Activationfiles** folder


![Upload File](./images/upload-activation-file.png 'Upload File')

7. Browse to select the file downloaded and then click **Upload**. Once the file is in the portal go to the Virtual Machine, connect to the **Microsoft Azure Storage Explorer** and refresh the container to see the file.

8. Select the File and click on **Download**.

![Upload File](./images/dowloand-file.png 'Upload File')


9. Go to Azure Defender Portal, select **System Settings** and then, **Reactivation**
![Reactivate](./images/reactivate.png 'Reactivate')


10. In hte new window, select **Upload**, **Browse File**, select the file you jsut downloaded, then **Open** and **Activate**, **Ok** to the instructions


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
