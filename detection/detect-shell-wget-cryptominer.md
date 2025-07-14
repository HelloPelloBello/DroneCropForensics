# Detection Rule: Crypto Miner Download via Wget

## What it Does

This rule detects when a command runs `wget` to download a cryptominer from a suspicious website (`badsite.example.com`). This is usually the attacker downloading malware.

## Why I Made This Rule

Since the attacker in this project downloaded a crypto miner, I wanted to catch that specific step. I searched for commands that include `wget` and the bad domain.

## How I Made This Rule

I looked at shell command logs and learned how attackers use `wget` to pull malware. Then, I combined that with the specific cryptominer URL from the incident to make this rule.

## How It Helps

It gives early notice of malicious downloads, so defenders can stop the attack before it uses resources or causes harm.

---

## Sigma Rule Code

```yaml
title: Crypto Miner Download via Wget
id: a2b1c55e-daf2-4c9e-8e59-4452fa3f2e21
status: test
description: Detects suspicious file downloads using wget from known bad domains.
author: HelloPelloBello
logsource:
  product: linux
  service: shell
detection:
  selection:
    command|contains:
      - 'wget'
      - 'cryptominer'
      - 'badsite.example.com'
  condition: selection
level: critical
tags:
  - attack.resource-development
  - attack.command-and-control
  - attack.t1105
