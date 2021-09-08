# Azure Defender for IoT/OT Security
# ***WORK IN PROGRESS, NOT TO SHARE***

**Hands-on lab workshop, Azure Defender for IoT/OT Security.**



August 2021.

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2020 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.


</br>

## **Audience:** ##

Teams working in projects related to Connected Devices, Smart Places, Factory of the Future, Industrial IoT, Energy, Oil and Gas.
  
  **Ideal attendee will be:**

   - Security Teams 
   - Operational Technology/Engineering(ICS)
		(Personal securing facilities such as factory floor, substations, oil and gas facilities.)

  **Industries:**
    - Energy 
	  - Utility
	  - Manufacturing
	  - Oil & Gas

  **What to expect:**
  - Session: This session is 100% Hands-on, no previous knowledge in Azure is required, you will learn by doing, it is important you are a person with Security experience or an Industrial consrol system engineering working in facilities. You will work with us all day, block any distractions during this day. Explanations will happening while we are building the solution.

    **The session will not be recorded**
  </br>

  - **IMPORTANT**: After the session, you will be able to configure Azure Defender in your facility to assess your own evironment, you will have a period of 15 days to schedule a call with Microsoft cybersecurity teams to assess your findings and guide through the process at no charge.

</br>

## **Date:** ##

- Americas: Oct/21/2021
- Time: 9am to 5pm EST Time

This workshop is **by invitation only**, Azure Passes will be provided as part of the training to make sure all the attendees can complete the labs without issues.


## **Contact Info:** ##

For any questions please send an email to:
iotacademy@microsoft.com

This workshop is delivered by SME in IoT and Cybersecurity at Microsoft.


</br>

## **Azure Defender Vocabulary** ## 

- Sensor: Linux machine, physical hardware running Azure defender connected to the network. 
- Manager: Linux machine, physical hardware running Azure defender connected to the network. It connects to multiple sensors to summarize data, alerts across multiples systems, carries the PCAP Configuration and new updates. Central Manager can be used to update the sensor's version and threat intelligence, can connect to many SIEM systems if needed also.
- IoT: Internet of the things. Modern, new standards connected devices
- OT: Operational Technology, old equipment and technology (i.e. conveys belts, PLCs).
- Brownfield devices: Type of legacy equipment and legacy software tht performs discrete function in isolation, usually nobody is willing to modify texisting, well-functioning legacy assets. 
- ICS: Industrial Control systems
- Greenfield devices: New and smart "cyber-physical systems", supporting new software landscape such as open communication protocols and open standards such as MQTT, REST APIs, AMQP, OPC-UA, MTConnect and CodeSys
- IIoT: Industrial IoT.
- SIEM: Security Information and event management.
- XDR: Cross detection and response
- Section 52: Microsoft Team dedicated to search for threads in the IoT and OT World.
- PCAP file: Packet Capture or PCAP (also known as libpcap) is an application programming interface (API) that captures live network packet data from OSI model Layers 2-7.
- Zero Trust Principles: Assume breach, verify explicitly, use least privilege access(identity at network)
- Purdue Model
    - Level 0 - Process: Phisical Machinery(actuators, pumps, cutters, mechanical arms, etc).
    - Level 1 - Basic Control
    - Level 2 - Supervisory Control
    - Level 3 - Site operations, computers such as linux providing site information to operators
    - Level 4 - IT Environments
    - Level 5 - IT Environments.



      ![Purdue model](./images/ot-deployments.png 'Purdue Model')









