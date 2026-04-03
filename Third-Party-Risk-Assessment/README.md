# Third-Party Risk Management (TPRM): Vendor Security Assessment

## Objective
The objective of this project was to conduct an Open-Source Intelligence (OSINT) security audit on a mock third-party vendor (a technology university). By evaluating their public-facing infrastructure, I simulated the vendor onboarding process used by financial institutions to assess supply chain risk, identify vulnerabilities, and ensure compliance with enterprise security frameworks.

## Skills & Technologies Used
* **Risk Domains:** Third-Party Risk Management (TPRM), Supply Chain Security, Vulnerability Assessment
* **Auditing Tools:** Qualys SSL Labs, MXToolbox, Mozilla HTTP Observatory
* **Security Protocols Evaluated:** TLS/SSL Encryption, DMARC (Email Authentication), HTTP Security Headers

## Audit Methodology & Findings

### 1. Cryptographic Security & Encryption (SSL/TLS) - [Status: PASS]
To evaluate data-in-transit protections, I utilized Qualys SSL Labs to inspect the vendor's web server configuration. The vendor demonstrated a strong cryptographic posture, scoring an overall 'A' grade. The server successfully supports modern TLS 1.3 protocols and utilizes robust cipher strengths (256-bit ECDSA), meeting enterprise banking standards for encrypted communications.

<img width="940" height="865" alt="image" src="https://github.com/user-attachments/assets/245d5600-a703-4226-90d7-26de82643264" />


### 2. Email Spoofing & Phishing Susceptibility (DMARC) - [Status: PASS]
Business Email Compromise (BEC) via third-party vendors is a critical attack vector. I queried the vendor's DNS records using MXToolbox to verify their email authentication policies. The audit confirmed the vendor has a valid DMARC record published with a `p=quarantine` policy enforced. This successfully mitigates the risk of threat actors spoofing the vendor's domain for phishing campaigns.

<img width="940" height="559" alt="image" src="https://github.com/user-attachments/assets/570453cb-a9b1-4904-ac65-359d0913209c" />


### 3. Web Application Security Headers - [Status: FAIL / CRITICAL RISK]
To assess the vendor's baseline defense against client-side vulnerabilities, I executed a scan via Mozilla Observatory. The vendor received a failing 'F' grade (0/100) due to a severe lack of foundational HTTP security headers. 

Key missing controls include:
* **Strict-Transport-Security (HSTS):** Missing, leaving users vulnerable to Man-in-the-Middle (MITM) downgrade attacks.
* **Content-Security-Policy (CSP):** Missing, creating a high susceptibility to Cross-Site Scripting (XSS) and data injection attacks.
* **X-Frame-Options:** Missing, allowing the site to be embedded in malicious iframes (Clickjacking).

<img width="940" height="680" alt="image" src="https://github.com/user-attachments/assets/06bf4757-15eb-46e1-afaa-a8149b121000" />

<img width="940" height="806" alt="image" src="https://github.com/user-attachments/assets/d69e0306-9ad9-45be-a543-6cfa08cebfb7" />


## GRC & Business Value Takeaway
This assessment highlights the critical necessity of "Trust but Verify" in Supply Chain Risk Management. Despite operating in the technology sector and possessing strong backend encryption, the vendor exhibited critical client-side vulnerabilities. 

In a real-world enterprise scenario, this vendor would **not** be cleared for immediate corporate onboarding. The GRC team would issue a formal remediation request, mandating the implementation of HSTS, CSP, and X-Frame-Options headers before any vendor contracts are finalized or API integrations are authorized.
