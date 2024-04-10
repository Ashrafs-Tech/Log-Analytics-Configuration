# Log Analytics Configuration

![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/3027cd4c-54c2-49ab-ac92-f9452ca41b4c)

## Intro

In this step, I will finished the configuration to allow the logs from the virtual machine to be sent into the Log Analytics Workspace.


## Azure Storage Account

To begin, I will a create an Azure storage account. Think of this like an enterprise Google Drive. It's a place where you can store files with a lot more and features. This is needed to store the Network Security Groups Flow Logs.

A Network Security Group is essentially a firewall that monitors traffic coming in and going out for the virtual machine. It can also record malicious traffic. These logs will be stored in Azure Storage account.

To do this:
- I will go to the Azure portal and type in "Storage Account"
- Clicked "Create Storage Account"
- I put it in the same region as the Linux and Windows machine
- I named it "syberlab009"

![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/714bf191-c817-4da7-87db-2bc4da63f300)


## Enable Flow Logs

Now I will enable Flow Logs for both Network Security groups.

To do this:
- I typed in Network Security Group in the Azure Portal.
- Selected the Windows virtual machine
- Scrolled down to NSG flow logs
- Clciked "Add Resourse" because I can make both Flow Logs for Windows and Linux virutal machine.
- Comfirm Selection
- Selected the Storage account syberlab009

![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/b802c090-5732-43fe-84bd-a6852d8a3a4b)
![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/15dea826-dd9c-41fe-ab59-d5f0c4f0ac0e)
![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/6e73489d-04b7-48d3-a978-258c65fc3a92)

- In the Analytics section:
  * I selected version 2
  * I also clicked Enabale Traffic Analytics
    - This is where Defender for Cloud will analyze the traffic and it will determine which traffic is malicous.
    - I set it to every 10 mins
    - I selected LAW-Cyber-Lab-Ver1 as the Log Analytics Workspace
- Clicked 'Review and Create"

![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/7a5ef378-d33b-4295-80f7-c2d82c9decd2)
![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/72b0ddfe-82a5-40da-a32a-c1e2c1b162b9)

## Configure Data collection rules

In the Log Analytics Workspace, I will configure the rules in Data Collection.

The data collection rule will work in conjuction with Microsoft Defender for Cloud.

It will specify which logs from the virutal machines will be sent to the Log Analytics Workspace.

To do this: 
- Go to Log Analytics Workspace
- Clicked on LAW-Cyber-Lab-Ver1
- Selected "Agents"
- Clicked on Data Collection Rules

![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/76852e68-eef2-4836-b144-e589b7efecaa)

Now to create the rule:
- I named the rule "dcr-all-vms"
- Placed it in the same reigon
- For the platform type, I selected "All"
  *This way, I can collect from Windows and Linux virtual machine.

![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/66df5210-8b37-4dfd-bd18-c068082ae1f7)


- Clicked on "Next"
- Then clicked on "Add resources"

![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/26c53312-eafe-4441-93d8-40cdd1f07040)

- Expand RG-Cyber-Lab
- Selected both Windows and Linux virtual machine
- Then clicked "Apply"

  ![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/eb448376-a92c-4797-a673-54b44fa2f61b)

- In the "Collect and deliver", I clicked " Add data source
- For the Data source type, I selected Linux Syslog
  * From here, I specified that the Linux "Log_Auth" will be collected. It will show the ssh failure attempts.
  * I selected "LOG_DEBUG".
  * Then forward it to the Log Analytics Workspace

![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/c2b5e8b4-5ec6-4022-a121-a997fead2f8a)
![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/903a6865-9c37-4bff-be25-3b9d486d3c99)


- After that, I clicked "Add data source" again.
- The data source type is "Window Event Logs"
- I selected the Information log from Application
  * That was selected because when I was configuring for the SQL database; the SQL logs appear in the Application Event Log under Information
- I also selected "Aduit success" and "Audit failure" under Security
  * When someone tries to Remote Desktop into my Windows virtual machine, successes and failures get logged into the Security Log
- It will be forwarded to the Log Analytics Workspace

![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/5277ddae-e084-4428-ab67-562858221723)
![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/99bf4557-744f-489c-bdcd-c582a1449b05)


## Step 5 is done

- Storage account has been created
- Network Security Group Flow Logs have been enabled
- Data Collection rules have been configured for Windows and Linux virutal machines 
  
![image](https://github.com/Ashrafs-Tech/Log-Analytics-Configuration/assets/166546026/31028c01-9983-4f61-a77a-f804d3fbb82a)





















