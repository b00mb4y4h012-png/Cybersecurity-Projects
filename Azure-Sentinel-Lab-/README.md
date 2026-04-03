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

[Insert Screenshot 1: NSG Rules Here]

Additionally, I disabled the Domain, Private, and Public profiles in the host-based Windows Defender Firewall. This ensured the VM would respond to ICMP (ping) requests and remain highly discoverable to automated internet scanners.

[Insert Screenshot 4: Windows Firewall Here]

### 2. Telemetry Ingestion & Log Analytics
Once the honeypot was live, it immediately began receiving unauthorized login attempts. I utilized Azure's Log Analytics Workspace to collect these security events. Using Kusto Query Language (KQL), I filtered the logs specifically for Windows Event ID 4625, which indicates a failed logon attempt. 

[Insert Screenshot 2: KQL Query & Logs Here]

### 3. Attack Visualization 
By mapping the ingested log data within Azure Sentinel, I was able to visualize the origin of the attacks on a global map. The telemetry revealed a high volume of continuous brute-force RDP (Remote Desktop Protocol) attempts. 

[Insert Screenshot 3: Attack Map Here]

## Key Findings & Security Takeaways
During the observation period, the honeypot was targeted by thousands of unauthorized access attempts globally. The most significant cluster of attacks originated from Poland, with over 21.7k logged attempts, followed by scanning activity from the UK and France.

**GRC & Remediation Perspective:**
This lab practically demonstrates the immediate risk of exposing RDP (port 3389) directly to the internet. To secure a similar enterprise environment, the following mitigating controls must be applied:
* **Network Segmentation & Access Control:** Restrict NSG inbound rules to specific, trusted IP addresses rather than an `Any/Any` configuration.
* **Secure Remote Access:** Implement Azure Bastion or a VPN for remote administration instead of exposing management ports to the public internet.
* **Identity & Access Management (IAM):** Enforce Account Lockout Policies to disrupt brute-force attempts and mandate Multi-Factor Authentication (MFA) for all administrative accounts.
