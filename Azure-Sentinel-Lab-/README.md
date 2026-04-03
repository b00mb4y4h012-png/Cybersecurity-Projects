# Azure Cloud SIEM & Honeypot Deployment

## Objective
The goal of this project was to deploy a cloud-based Security Information and Event Management (SIEM) system using Microsoft Azure Sentinel. I provisioned a deliberately vulnerable Windows Virtual Machine to act as a honeypot, exposed it to the public internet, and ingested the resulting telemetry into a Log Analytics Workspace. This allowed me to query the logs and visualize live, global brute-force attacks in real-time.

## Skills & Technologies Used
* **Cloud Infrastructure:** Microsoft Azure (Virtual Machines, Resource Groups)
* **Security Operations (SecOps):** Microsoft Sentinel (SIEM), Log Analytics Workspace
* **Network Security:** Network Security Groups (NSGs), Windows Defender Firewall configuration
* **Log Analysis:** Kusto Query Language (KQL), Event Viewer (Windows Security Logs - Event ID 4625)

## Deployment & Configuration Process

### 1. Intentional Vulnerability Exposure
To attract threat actors, I configured the Azure Network Security Group (NSG) to be overly permissive. I created a custom inbound rule (`dangerakacool_allowanycustomanyinbound`) allowing `Any` traffic from `Any` source port and IP address to access the VM. 

<img width="940" height="316" alt="image" src="https://github.com/user-attachments/assets/e56ccdf6-29f2-431c-a169-979839982a36" />


Additionally, I disabled the Domain, Private, and Public profiles in the host-based Windows Defender Firewall. This ensured the VM would respond to ICMP (ping) requests and remain highly discoverable to automated internet scanners.

<img width="940" height="614" alt="image" src="https://github.com/user-attachments/assets/da46dfad-72d4-418d-893b-09b33442c9a9" />


### 2. Telemetry Ingestion & Log Analytics
Once the honeypot was live, it immediately began receiving unauthorized login attempts. I utilized Azure's Log Analytics Workspace to collect these security events. Using Kusto Query Language (KQL), I filtered the logs specifically for Windows Event ID 4625, which indicates a failed logon attempt. 

<img width="940" height="521" alt="image" src="https://github.com/user-attachments/assets/6a0531fb-e8a4-4730-80dc-18907c4035d7" />


### 3. Attack Visualization 
By mapping the ingested log data within Azure Sentinel, I was able to visualize the origin of the attacks on a global map. The telemetry revealed a high volume of continuous brute-force RDP (Remote Desktop Protocol) attempts. 

<img width="940" height="716" alt="image" src="https://github.com/user-attachments/assets/cbaaf817-57b3-4968-8b8c-fea44300170f" />


## Key Findings & Security Takeaways
During the observation period, the honeypot was targeted by thousands of unauthorized access attempts globally. The most significant cluster of attacks originated from Poland, with over 21.7k logged attempts, followed by scanning activity from the UK and France.

**GRC & Remediation Perspective:**
This lab practically demonstrates the immediate risk of exposing RDP (port 3389) directly to the internet. To secure a similar enterprise environment, the following mitigating controls must be applied:
* **Network Segmentation & Access Control:** Restrict NSG inbound rules to specific, trusted IP addresses rather than an `Any/Any` configuration.
* **Secure Remote Access:** Implement Azure Bastion or a VPN for remote administration instead of exposing management ports to the public internet.
* **Identity & Access Management (IAM):** Enforce Account Lockout Policies to disrupt brute-force attempts and mandate Multi-Factor Authentication (MFA) for all administrative accounts.
