<h1>Honeypot (Azure)</h1>

<h2>Brief Objective</h2>
The goal of this project was to simulate a honeypot in the cloud by configuring an Azure virtual machine and integrating it with Microsoft Sentinel for security monitoring. I aimed to simulate a brute force attack via RDP, to detect successful sign-ins through a custom alert rule. By setting up a Log Analytics workspace and using the Windows Security Events connector, I ensured that any successful attack attempts were captured, allowing for scheduled monitoring and alerting within Microsoft Sentinel. <br />


<h2>Skills Learned</h2>

- <b>Microsoft Sentinel Integration</b> 
- <b>Custom Alert Rule Creation</b>
- <b>Security Event Simulation and Monitoring </b>

<h2>Steps</h2>

**Virtual Machine Setup:** <br/>
Within the Azure portal, I used the navigation search bar tool to locate and select Virtual machines. I then chose the option for an “Azure Virtual Machine with preset configuration” to streamline the setup process. <br/>

<br />

**Virtual Machine Configuration:** <br/>
I configured the virtual machine with the following parameters, leaving the remaining settings at their default values: <br />
Resource Group: Created a new resource group named myvm_group to serve as the container for all associated resources. <br />
Virtual Machine Name: myVM <br />
Region: East US (US East) <br />
Availability Options: Zone 2 <br />
Image: Windows 10 Pro, version 22H2 - x64 Gen2 <br />
Size: Standard_D4s_v3 (4 vCPUs, 16 GiB memory) <br />
Administrator Account: <br />
Username: “Example” <br />
Password: “Example123” <br />
Inbound Ports: RDP (3389) - I left the RDP port open temporarily for testing purposes to allow remote traffic. <br />

**Deployment:** <br/>
After reviewing the configuration, I clicked Create, and the virtual machine was successfully deployed within a few minutes. <br />
![1](https://github.com/user-attachments/assets/20f9815e-ee4a-4454-b09b-dbcaa9525177)


**Microsoft Sentinel Setup:** <br/>
Next, I navigated to Microsoft Sentinel and followed the guided process to create a Log Analytics workspace. I ensured that I used the same resource group, "myvm_group," as the one associated with the virtual machine. The instance was named TW-LogAnalytics, and the region was set to East US, consistent with the virtual machine's location. This was important to avoid any potential lag or delays caused by splitting resources across different regions.<br/>
![2](https://github.com/user-attachments/assets/753a2a75-77f2-4bf2-970a-9cd262ded03e)
<br />

**Log Analytics Workspace Configuration:** <br/>
Once the Log Analytics workspace was created, I configured the virtual machine to forward its event logs to this workspace. This enabled Microsoft Sentinel to pull the data from the virtual machine endpoint and display it in the overview section GUI/dashboard. <br/>

<br />

**Data Connector Setup:** <br/>
To facilitate the log forwarding, I configured a data connector. From the content hub, I installed the Windows Security Events connector, which utilizes the Azure Monitoring Agent (AMA) to collect security-related data. <br/>

<br />

**Data Collection Rule Configuration:** <br/>
After successfully installing the Windows Security Events via AMA, I opened the connector page and created a new data collection rule. I completed the required fields, selecting the resource group myvm_group and the virtual machine myVM from which to collect the event logs. Finally, I chose the ‘All Security Events’ option to ensure comprehensive event streaming.<br />

<br />

**Create Microsoft Sentinel Alert Rule:** <br/>
From Microsoft Sentinel, I navigated to Logs and selected New alert rule to create a custom alert. I named the rule "Successful Local Sign-Ins," set the severity to Medium, and assigned the MITRE ATT&CK tactic of Initial Access. <br />

<br />

**Configure Rule Query:** <br/>
I configured the rule query to run every 5 minutes, with a lookup period of the same duration. The alert rule was set to start running automatically, with an alert threshold of greater than 0. I also selected the option to group events into a single alert to reduce noise and ensure more efficient detection.
![3](https://github.com/user-attachments/assets/682d5e81-51c4-444d-afb9-ccdaeac66783) <br />
I specified the query to trigger an alert when a successful RDP sign-in occurred, simulating a brute force attack by manually connecting to the virtual machine via RDP. As a result, a new incident appeared in the GUI or Incident subsection, indicating a successful local sign-in and the honeypot is working as intended. <br />
![4](https://github.com/user-attachments/assets/dbce85e9-3f29-47d8-a8a6-9b104ad44b90)
![5](https://github.com/user-attachments/assets/9eaaa09d-fd67-4df4-9bb5-6e3b688bd855)

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
