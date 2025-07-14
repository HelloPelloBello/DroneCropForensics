\# Threat Actor Hypothesis – DroneCropForensics Incident



This section theorizes the motivations, capabilities, and behaviors of the adversary based on observed evidence. Attribution is avoided due to lack of unique indicators; however, threat classification is attempted based on behavior patterns.



\## Threat Profile



The threat actor in this simulation exhibits characteristics aligned with financially motivated cybercriminals, operating at the lower-to-mid technical sophistication level.



\## Behavior Analysis



\### Opportunistic Reconnaissance



\- The initial access vector relied on identifying exposed AWS credentials on a public GitHub repository.

\- This suggests the use of automated scanners or GitHub dorking tools to find sensitive information committed to version control.

\- No social engineering or advanced intrusion techniques were observed.



\### Cloud Infrastructure Enumeration



\- Post-compromise activity included the use of `DescribeInstances` and `StartInstances` APIs — standard reconnaissance steps to identify and activate EC2 infrastructure.

\- These actions align with MITRE ATT\&CK's \*\*Cloud T1580 (Cloud Infrastructure Discovery)\*\* and \*\*T1538 (Cloud Service Dashboard)\*\*.



\### Payload Deployment – Cryptojacking



\- The attacker deployed a known cryptomining package from an external domain, configured for quick execution.

\- Resource hijacking via mining has low barrier to entry and provides immediate monetary gain through exploitation of cloud compute.



\### Application-Layer Sabotage



\- The adversary deleted a critical web service script (`upload.php`), which broke drone upload functionality.

\- This action goes beyond typical cryptojacking behavior, indicating either:

&nbsp; - Intentional sabotage (to punish or disrupt the target)

&nbsp; - Careless behavior with no concern for operational impact



\## Overall Threat Model



This attack reflects a \*\*"low sophistication, high impact"\*\* intrusion — an increasingly common trend in cloud security incidents.



\- It did not involve zero-day exploits, rootkits, or evasive malware.

\- The breach succeeded entirely due to:

&nbsp; - Insecure development practices (hardcoded credentials)

&nbsp; - Inadequate access monitoring

&nbsp; - Overprivileged IAM roles



These characteristics suggest a wide-open attack surface that was trivially exploited.



