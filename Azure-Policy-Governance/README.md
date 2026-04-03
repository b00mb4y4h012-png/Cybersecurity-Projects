# Cloud Governance & Compliance: Enforcing Azure Policy

## Objective
The objective of this project was to implement "Governance as Code" by deploying Microsoft Azure Policies to enforce compliance standards across a cloud environment. By mandating specific resource tags, this lab demonstrates how to proactively prevent the deployment of non-compliant infrastructure and ensure strict adherence to corporate governance frameworks.

## Skills & Technologies Used
* **Cloud Infrastructure:** Microsoft Azure
* **Governance, Risk, and Compliance (GRC):** Azure Policy, Resource Tagging, Compliance Auditing
* **Preventative Security:** Policy Enforcement, Validation Logic

## Deployment & Configuration Process

### 1. Policy Definition and Assignment
To establish accountability and regulatory tracking within the cloud tenant, I configured a foundational governance rule. I navigated to Azure Policy Definitions and assigned the `Require a tag on resources` policy to the active subscription. I parameterized the policy to specifically mandate a `Created By` tag, ensuring all future resources are explicitly tied to an owner for audit purposes.

<img width="940" height="415" alt="image" src="https://github.com/user-attachments/assets/8b36fb50-a6e6-4971-8289-f18648fbc135" />


### 2. Compliance Enforcement & Validation Testing
To test the efficacy of the preventative control, I attempted to provision a new Azure resource (a Public IP address) *without* the mandated `Created By` tag. 

As intended, Azure's compliance engine intercepted the deployment. The action was actively blocked, generating a `Validation Failed` error and displaying the custom non-compliance message. This confirmed that the technical guardrails were successfully preventing policy violations in real-time.

<img width="940" height="487" alt="image" src="https://github.com/user-attachments/assets/f57c6414-c1fb-46a0-a864-c363fa2f9136" />


### 3. Remediation and Successful Deployment
To achieve compliance, I remediated the resource configuration by navigating back to the deployment parameters and injecting the required `Created By` tag with my credentials. Upon re-running the validation check, the resource passed the policy requirements and was successfully provisioned.

<img width="940" height="656" alt="image" src="https://github.com/user-attachments/assets/6c586aee-5229-4a04-9230-2a1e4aec244a" />


## GRC & Business Value Takeaway
This project practically demonstrates the core function of Cloud Governance. In an enterprise environment, relying on manual audits is inefficient and highly prone to human error. By leveraging Azure Policy, organizations can:
* **Prevent Regulatory Fines:** Automatically block the creation of non-compliant resources (e.g., unencrypted databases or resources in unauthorized geographic regions).
* **Automate Auditing:** Ensure every asset deployed in the cloud conforms to internal security standards (like ISO 27001) before it even goes live.
* **Enforce Accountability:** Use mandatory tagging to accurately track cloud spend, ownership, and incident response contacts across different business units.
