# Microsoft Defender for IoT/OT Security

**Hands-on lab workshop, Microsoft Defender for IoT/OT Security.**

January 2022.

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2021 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

</br>

## **Audience:** ##

Teams working in projects related to Connected Devices, Smart Places, Factory of the Future, Industrial IoT, Energy, Oil and Gas.
  
**Ideal attendee will be:**
   - Security Teams 
   - Operational Technology/Engineering(ICS) - (Personnel securing facilities such as factory floors, substations, oil and gas facilities).

**Industries:**
   - Energy
   - Utility
   - Manufacturing
   - Oil & Gas 

**What to expect:**
  - Session: This session is 100% Hands-on, no previous knowledge in Azure is required. You will learn by doing. It is important you are a person with Security experience or that you have an Industrial Control System Engineering background, working in facilities. You will work with us all day. Please block any distractions during this day. Explanations will happening while we are building the solution.

    **This session will not be recorded**

</br>

## **Dates:** ##

- Americas: Oct/21/2021 (Time: 9am to 5pm EST Time)
- EMEA: Feb/01/2022 (Time: 9am to 5pm CET Time)

This workshop is **by invitation only**. Azure Passes will be provided as part of the training to make sure all the attendees can complete the labs without issues.

>NOTE: It is possible to run the workshop on your own if you already have an existing Azure subscription. In this case you will be charged for running some of the services used in this HOL.

</br>

## **Contact Info:** ##

For any questions please send an email to:
iotacademy@microsoft.com

This workshop is delivered by SMEs in IoT and Cybersecurity at Microsoft.

</br>

## **Microsoft Defender for IoT Vocabulary** ## 

**Sensor**: Linux machine, physical hardware running Microsoft Defender for IoT connected to the network.

**Manager**: Linux machine, physical hardware running Microsoft Defender for IoT connected to the network. It connects to multiple sensors to summarize data, alerts across multiples systems, carries the PCAP Configuration and new updates. Central Manager can be used to update the sensor's version and threat intelligence, can also connect to many SIEM systems if needed.

**IoT**: Internet of Things. Modern, new standard connected devices.

**IIoT**: Industrial IoT.

**OT**: Operational Technology, old equipment and technology (e.g, conveyer belts, PLCs).

**Brownfield devices**: Type of legacy equipment and legacy software that performs discrete function in isolation, usually nobody is willing to modify existing, well-functioning legacy assets. 

**ICS**: Industrial Control systems

**Greenfield devices**: New and smart "cyber-physical systems", supporting new software landscapes such as open communication protocols and open standards such as MQTT, REST APIs, AMQP, OPC-UA, MTConnect and CodeSys.

**SIEM**: Security Information and Event Management

**Section 52**: Microsoft Team dedicated to search for threats in the IoT and OT World.

**PCAP file**: Packet Capture or PCAP (also known as libpcap) is an application programming interface (API) that captures live network packet data from OSI model Layers 2-7.

**Zero Trust Principles**: Assume breach, verify explicitly, use least privilege access (identity at network).

**XDR**: Cross detection and response

**Purdue Model**
- Level 0 - Process: Physical Machinery (actuators, pumps, cutters, mechanical arms, etc).
- Level 1 - Basic Control
- Level 2 - Supervisory Control
- Level 3 - Site operations, computers such as linux providing site information to operators
- Level 4/5 - IT Environments
  
  ![Purdue model](./images/ot-deployments.png 'Purdue Model')

