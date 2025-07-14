# DroneCropForensics: A Cloud DFIR Case Study on an AgriTech Drone Platform Breach

## Introduction

This project is a detailed investigation of a simulated cybersecurity breach targeting a fictional AgriTech startup. The startup operates a cloud-based drone platform that scans crop fields and stores images in Amazon S3 buckets. Unfortunately, due to a careless mistake, a developer leaked AWS credentials publicly on GitHub. This exposed secret allowed an attacker to break into the system, steal sensitive data, and cause significant damage.

I built this project to learn how cloud breaches happen in real life and how a digital forensics and incident response (DFIR) analyst investigates such attacks step-by-step. By creating realistic logs, detection rules, and analysis, I aimed to demonstrate my understanding of cloud security threats and incident response workflows.

---

## What Happened in the Incident?

Here is the sequence of events that I simulated based on common attack tactics:

1. **Credential Leak:** AWS access keys were accidentally published in a public GitHub repository.  
2. **Reconnaissance:** The attacker found the leaked keys and started scanning the cloud infrastructure.  
3. **Data Exfiltration:** Using the stolen keys, the attacker downloaded crop images from the S3 bucket, stealing valuable data.  
4. **Server Compromise:** The attacker gained SSH access to the EC2 instance hosting the drone API.  
5. **Payload Deployment:** A cryptominer was downloaded and executed on the server, abusing resources for cryptocurrency mining.  
6. **Service Disruption:** The attacker deleted the critical API file (`upload.php`), breaking the drone image upload functionality and causing downtime.

---

## What You Will Find in This Repository

- **Simulated Logs:** CloudTrail logs for AWS activities, Linux auth logs for SSH events, and shell command history capturing the attacker's actions.  
- **Detection Rules:** Sigma rules designed to detect the specific malicious activities during the attack, such as suspicious S3 downloads, unauthorized SSH access, malicious payload downloads, and file deletions.  
- **Indicators of Compromise (IOCs):** A consolidated list of IP addresses, malicious domains, compromised files, and suspicious commands used by the attacker.  
- **Detailed Observations:** Notes and explanations about attacker behavior and the impact of each step.  
- **Recommendations:** Practical security advice to prevent similar incidents, including secrets management, monitoring, and alerting best practices.

---

## Why I Created This Project

As a learner deeply interested in cybersecurity and cloud forensics, I wanted to challenge myself by creating a realistic incident response case study. Many tutorials stop at theory or fragmented examples, but I wanted to build an end-to-end investigation — from the initial breach to detection and remediation suggestions.

Through this project, I learned:

- How simple mistakes, like leaking AWS keys, can lead to devastating cloud breaches.  
- The importance of detailed log analysis to trace attacker actions accurately.  
- Writing effective detection rules requires understanding both attacker tactics and the environment.  
- How to communicate complex findings in clear, actionable ways to help defenders.

---

## How I Built the Project

My process included:

1. **Incident Simulation:** I designed the attack scenario and created fake but realistic logs that capture each attacker step.  
2. **Log Analysis:** I parsed logs carefully to extract attacker behaviors and timestamps, building a timeline of events.  
3. **Detection Engineering:** Using Sigma, I crafted rules to detect these malicious actions. I started from public templates, researched cloud threat techniques, and customized the rules to this scenario.  
4. **Reporting:** I documented my findings, insights, and recommendations in Markdown files to make the investigation easy to understand.  
5. **Continuous Improvement:** I iterated on rules and analysis to improve accuracy and reduce false positives.

---

## How This Project Can Help You

If you are:

- A beginner wanting to learn how cloud breaches happen and how to investigate them,  
- Interested in understanding how logs tell the story of an attack,  
- Looking to practice writing detection rules and forensic reports,  
- Curious about real-world applications of DFIR concepts in cloud environments,  

then this project can serve as a practical learning resource. You can explore the logs, read the detection logic, and see how attacker behaviors map to specific alerts.

---

## What I Learned and Why It Matters

Cloud environments are complex and constantly changing, but some risks remain constant:

- **Secrets Leaks:** Storing credentials in code or public repos is extremely risky and often the root cause of breaches.  
- **Monitoring and Detection:** Continuous monitoring with tools like AWS GuardDuty and custom detection rules is vital to catch attacks early.  
- **Incident Response:** Having a clear process and tools to analyze logs quickly can minimize attacker dwell time and reduce damage.  
- **Communication:** Clear documentation helps security teams understand incidents and act faster.

This project reinforced how important it is to combine technical skills with thoughtful analysis and communication.

---

## What’s Next?

I plan to expand this work by:

- Adding automation for detection and alerting pipelines,  
- Covering more cloud services like Lambda and RDS in investigations,  
- Simulating real-time alert generation and response scenarios,  
- Integrating findings with popular SIEM platforms to make detection practical.

---

## How to Use This Repository

- Review the logs to understand attacker actions in detail.  
- Study the Sigma detection rules to learn how to identify suspicious behavior.  
- Use the IOCs for threat hunting or SIEM testing.  
- Read the observations and recommendations to improve your cloud security knowledge.

---

## Connect With Me

I’m still learning and growing in cybersecurity and cloud forensics. If you want to share ideas, give feedback, or collaborate, feel free to reach out via GitHub.

Thanks for taking the time to explore my project. Every step forward counts!

---

*This project is a personal learning journey and not affiliated with any real company or organization.*
