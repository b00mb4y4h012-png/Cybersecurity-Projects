# Threat Intelligence & OSINT: Malware Analysis and MITRE ATT&CK Mapping

## Objective
The objective of this project was to leverage Open Source Intelligence (OSINT) tools to investigate a known Indicator of Compromise (IOC). I analyzed a malicious file hash, mapped its behavioral characteristics to the MITRE ATT&CK framework, and generated a high-level threat intelligence summary to aid in enterprise risk management.

## Skills & Technologies Used
* **Threat Intelligence Platforms:** VirusTotal, AlienVault Open Threat Exchange (OTX)
* **Frameworks:** MITRE ATT&CK Matrix
* **Security Operations:** OSINT gathering, IOC Analysis, Malware Behavior Profiling

## Investigation Workflow

### 1. Initial Indicator of Compromise (IOC) Triage
The investigation began with a SHA-256 file hash suspected of malicious activity. To establish a baseline reputation, I queried the IOC against the VirusTotal database. The platform's aggregate scanning engines overwhelmingly identified the file as a severe ransomware payload, specifically tied to the WannaCry family.

<img width="940" height="547" alt="image" src="https://github.com/user-attachments/assets/cd94dead-483a-4d0d-a177-70f99bbed41f" />


### 2. Behavioral Profiling & MITRE ATT&CK Mapping
Understanding that simply identifying malware is insufficient for preventative defense, I pivoted to analyzing the payload's behavior. Utilizing sandbox execution data, I mapped the malware's capabilities directly to the MITRE ATT&CK framework. Key identified tactics included:
* **Execution:** Utilizing native APIs to run malicious code.
* **Defense Evasion:** Modifying the registry and hiding files to avoid detection.
* **Impact:** Encrypting data for impact (Ransomware behavior).

<img width="940" height="441" alt="image" src="https://github.com/user-attachments/assets/5e7ab5d5-7532-4f75-8aeb-62699e339329" />


### 3. Open Threat Exchange (OTX) Corroboration
To contextualize the threat within the broader cybersecurity landscape, I cross-referenced the IOC on AlienVault OTX. The community Pulses corroborated the initial findings, linking the hash to historic, large-scale ransomware campaigns targeting enterprise vulnerabilities (such as EternalBlue).

<img width="1851" height="937" alt="image" src="https://github.com/user-attachments/assets/9c39ce9c-be37-4409-966f-3153e37f325d" />


## GRC & Business Value Takeaway
This lab demonstrates the translation of raw technical data into actionable Risk Management intelligence. For an enterprise SOC or GRC team, this capability is critical for:
* **Proactive Defense:** Updating internal firewalls, EDRs, and SIEMs with known bad hashes and IPs before an attack occurs.
* **Risk Reporting:** Translating complex malware behaviors (via MITRE ATT&CK) into clear business risks for executive leadership.
* **Incident Preparedness:** Understanding adversary tactics to build better incident response playbooks and compliance checks.
