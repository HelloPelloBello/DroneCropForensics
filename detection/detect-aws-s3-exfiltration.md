\# Detection Rule: Suspicious S3 Data Exfiltration from Unusual IP



\## What it Does

This rule looks for multiple AWS S3 `GetObject` requests coming from an unusual IP address (91.203.119.5). It helps catch when someone might be stealing data from cloud storage.



\## Why I Made This Rule

I wanted to detect if someone is downloading sensitive data from S3 buckets without permission. Since leaked AWS keys were used in this incident, watching suspicious downloads is important.



\## How I Made This Rule

I started by learning about AWS CloudTrail events, especially the `GetObject` event that means someone downloaded a file from S3. Then, I matched the IP address we saw in the attack logs to filter out normal activity. I looked at public Sigma rule examples and adjusted them to fit the situation in this project.



\## How It Helps

It gives an early warning if someone is accessing your cloud storage in a suspicious way, so you can stop data leaks faster.



---



\## Sigma Rule Code



```yaml

title: Suspicious S3 Data Exfiltration from Unusual IP

id: 1f5e9c25-0a44-4fc3-ae29-7c5b1fd425ee

status: experimental

description: Detects multiple S3 GetObject requests from unusual IPs indicating possible data exfiltration.

author: HelloPelloBello

logsource:

&nbsp; product: aws

&nbsp; service: cloudtrail

detection:

&nbsp; selection:

&nbsp;   eventName: GetObject

&nbsp;   sourceIPAddress|ip:

&nbsp;     - 91.203.119.5

&nbsp; condition: selection

level: high

tags:

&nbsp; - attack.collection

&nbsp; - attack.t1530

&nbsp; - exfiltration



