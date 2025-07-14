# Detection Rule: EC2 SSH Access from Unknown IP

## What it Does

This rule detects when someone logs into an EC2 server via SSH from an IP address we don’t usually see (91.203.119.5). This usually means someone might have broken in.

## Why I Made This Rule

I learned that SSH is a common way attackers get inside servers. So I wanted to catch any unusual login early, especially from the suspicious IP found in the attack.

## How I Made This Rule

I studied Linux authentication logs and found that “Accepted publickey” messages show successful SSH logins. Then I filtered for the attacker IP. I checked public Sigma rules for SSH and made one specific to this project’s case.

## How It Helps

It alerts if an unknown user accesses your server, so you can check and stop any possible attacks.

---

## Sigma Rule Code

```yaml
title: EC2 SSH Access from Unknown IP
id: 6b13d3c9-b18c-4d33-8103-f0639f3fce6c
status: stable
description: Detects SSH login from an external IP after an EC2 instance was started.
author: HelloPelloBello
logsource:
  product: linux
  service: auth
detection:
  selection:
    message|contains: 'Accepted publickey'
    src_ip: 91.203.119.5
  condition: selection
level: high
tags:
  - attack.initial-access
  - attack.t1078
  - persistence
