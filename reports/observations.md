# Observations – DroneCropForensics Incident

## What I Observed

While digging through the logs and trying to understand what happened in this simulated attack, here’s what I noticed and learned. I’m still learning, so this is my honest take on the whole incident.

---

## Main Things I Noticed

### 1. Leaked Credentials Were the Starting Point

The whole thing started because someone accidentally put AWS keys in a `.env` file on a public GitHub repo. This is such a simple but big mistake, and I see now how easy it is for attackers to find secrets if we’re not careful with how we manage them.

### 2. The Attacker Was Probably Using Automated Tools

From what I saw, the attacker didn’t do anything super fancy like social engineering or zero-day hacks. It looked like they used scripts or scanners to search GitHub for exposed secrets. This feels like a low-tech but effective way to break in if you leave the door open.

### 3. They Explored the Cloud Setup Using AWS APIs

Once they had the keys, they ran commands to check what EC2 instances were available and even turned on one that wasn’t running. This showed me how attackers can map out cloud environments pretty easily using standard AWS tools.

### 4. They Installed a Cryptominer on the Server

I saw commands where they downloaded and ran a cryptomining program. It seems their goal was mostly to make money by hijacking cloud computing power. That was interesting because it showed how cloud resources can be abused quietly.

### 5. They Also Broke the Drone Upload Service

Something I didn’t expect was that they deleted an important file for the drone upload API (`upload.php`). This caused the service to break. It made me think maybe the attacker wanted to cause trouble, or maybe they didn’t care about breaking things as long as they got their cryptominer running.

### 6. There Were Weak Security Controls

I noticed that the leaked keys had too many permissions, and there were no alarms or monitoring in place to catch unusual activity quickly. This helped the attacker move around without being stopped. It showed me how important it is to have strict access controls and monitoring.

---

## Why I Think These Matter

From this, I realized:

- We should **never put secrets like AWS keys in public repos** and use tools like AWS Secrets Manager instead.

- Giving only the minimum permissions needed (least privilege) is really important so attackers can’t do much if they get in.

- Setting up **continuous monitoring and alerts** would help detect bad things early and stop attackers faster.

- Having clear logs and investigation plans helps understand what went wrong and how to fix it.

---

## Final Thoughts

This exercise taught me how small mistakes can lead to big security problems. I also learned how attackers don’t always need fancy tools—sometimes just scanning public data is enough.

I want to keep learning how to build better defenses, catch attacks early, and understand the whole process from breach to recovery. This project was a great step in that journey.

---

*Thanks for reading my observations!*
