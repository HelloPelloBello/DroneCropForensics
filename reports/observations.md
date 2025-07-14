# Observations – DroneCropForensics Incident

## Overview

This section summarizes the key findings and insights derived from analyzing the logs, attack patterns, and overall impact of the incident simulated in the DroneCropForensics project. The observations highlight attacker tactics, techniques, and procedures (TTPs), as well as vulnerabilities exploited and consequences observed.

---

## Key Observations

### 1. Credential Exposure as the Primary Attack Vector

The initial breach was enabled by the accidental public exposure of AWS credentials in a `.env` file on a GitHub repository. This classic mistake remains one of the most common causes of cloud security incidents. It underscores the critical need for proper secrets management and code hygiene practices.

### 2. Automated and Opportunistic Threat Actor Behavior

The attacker demonstrated opportunistic behavior, likely leveraging automated tools to scan public repositories for leaked credentials. There was no indication of complex social engineering or zero-day exploit usage, indicating a low sophistication attacker relying on poor operational security.

### 3. Cloud Infrastructure Reconnaissance and Exploitation

Following credential discovery, the attacker conducted cloud infrastructure enumeration using AWS APIs such as `DescribeInstances` and `StartInstances`. These actions helped identify and activate EC2 instances to establish further access. This step reflects an understanding of cloud environments but is achievable with standard AWS CLI commands.

### 4. Deployment of Cryptomining Payload

The attacker deployed a cryptominer on the compromised EC2 instance. Cryptojacking is a financially motivated tactic that exploits cloud compute resources without the target’s knowledge. This behavior suggests the adversary’s primary goal was monetary gain, utilizing cloud resources as a commodity.

### 5. Intentional Service Disruption

Unlike typical cryptojacking incidents, the attacker deliberately deleted a critical API file (`upload.php`), causing the drone image upload service to fail. This sabotage could indicate malicious intent to disrupt business operations or negligent behavior without concern for collateral damage.

### 6. Inadequate Monitoring and Access Controls

The breach succeeded due to a combination of insecure development practices (hardcoded credentials), overprivileged IAM roles, and lack of continuous monitoring. The absence of alerts on anomalous API calls or SSH logins allowed the attacker to operate undetected for a period.

---

## Why These Observations Matter

Understanding these observations is vital for improving cloud security posture:

- **Secrets Management:** Implementing vaults and automated secrets rotation can prevent accidental exposure.

- **Principle of Least Privilege:** Restricting IAM roles to only necessary permissions reduces the blast radius.

- **Continuous Monitoring and Alerting:** Tools like AWS GuardDuty and CloudTrail alarms help detect and respond to suspicious activities promptly.

- **Incident Response Preparedness:** Having detailed logs and incident playbooks accelerates investigation and remediation.

---

## Reflection

This incident simulation serves as a valuable learning experience, showcasing how simple mistakes lead to significant security events and the importance of layered defenses. It emphasizes the evolving threat landscape in cloud environments and the need for vigilance, automation, and education to safeguard digital assets.

---

*End of observations.*
