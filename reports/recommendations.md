# Recommendations – Post-Incident Remediation



This section outlines specific, actionable security recommendations based on the findings of the DroneCropForensics investigation. The objective is to both mitigate the current compromise and harden the infrastructure against future breaches.



## 1. Immediate Key Revocation and Credential Rotation



- Revoke all IAM users and roles exposed via the `.env` file immediately.

- Rotate root account credentials and all long-lived keys used by the development team.

- Implement AWS Config rules to monitor for hardcoded credential usage and flag any future exposures.



## 2. Secrets Management Enforcement



- Completely phase out usage of hardcoded secrets in `.env` or source files.

- Migrate to AWS Secrets Manager, Parameter Store (SSM), or HashiCorp Vault for centralized, auditable, and role-based secret access.

- Add `git-secrets`, `truffleHog`, or `gitleaks` as pre-commit hooks to scan codebases before any push.



## 3. Enable AWS GuardDuty and CloudTrail Alerts



- Activate GuardDuty for continuous threat detection across AWS resources.

- Set CloudWatch alarms on suspicious API calls such as:

&nbsp; - `StartInstances`, `StopLogging`, `CreateUser`, `AttachRolePolicy`

&nbsp; - Anomalous `Describe\*` calls from new IPs

&nbsp; - Repeated failed login attempts

- Forward GuardDuty and CloudTrail logs to a central SIEM for long-term correlation.



## 4. IAM Least Privilege Review



- Audit and restrict all IAM policies with `\*:\*` permissions.

- Implement role-based access controls (RBAC) and follow least-privilege principles.

- Require MFA for all users and disallow use of root account for day-to-day operations.



## 5. Harden EC2 and Application Infrastructure



- Deploy endpoint monitoring agents like Wazuh, Osquery, or CrowdStrike Falcon on all EC2 nodes.

- Monitor file system integrity on critical paths such as `/var/www/html` using tools like Filebeat or AIDE.

- Enable systemd service auditing and bash history logging with remote log forwarding.



## 6. Secure CI/CD Pipelines



- Integrate secret scanning and SAST (Static Application Security Testing) into the CI/CD process.

- Prevent developers from committing secrets using signed commits and enforced code reviews.

- Validate all third-party dependencies using SBOMs (Software Bill of Materials) and supply chain tools like DependencyTrack or Sigstore.



## 7. Conduct Regular Cloud Security Drills



- Simulate credential leakage and run tabletop exercises for your incident response team.

- Automate response playbooks using AWS Systems Manager or Lambda to isolate EC2s automatically during suspected compromise.

- Benchmark your infrastructure using CIS AWS Foundations or AWS Well-Architected Framework.



