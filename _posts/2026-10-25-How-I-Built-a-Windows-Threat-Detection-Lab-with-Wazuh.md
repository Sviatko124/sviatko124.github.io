---
layout: post
date: 2026-10-25
author: Sviatko124
tags: Active-Directory Threat-Detection Wazuh
---
# How I Built a Windows Threat Detection Lab with Wazuh

What happens when someone enters the wrong password on a Windows computer? It might seem like a small event, but in cybersecurity, even a failed login can be worth investigating.

As part of my cybersecurity learning journey, I built an Active Directory threat detection lab using **Wazuh SIEM** to explore how security events can be detected, reviewed, and investigated.

## What is this project?

A Security Information and Event Management (SIEM) platform helps security teams collect and analyze activity from computers and other systems. It can surface events that may require further investigation.

For this project, I created a small virtual lab containing:

- **Windows Server:** Provides Active Directory domain services.
- **Windows client:** A domain-joined computer where authentication events are generated.
- **Wazuh SIEM:** Collects and displays security events so they can be investigated.

The goal was to demonstrate a practical example of how a SOC analyst might investigate a Windows authentication event.

## Putting Wazuh to the test

I performed two intentional failed logon attempts in the lab and then reviewed the resulting authentication failures in the Wazuh dashboard.

![Wazuh dashboard displaying authentication failures](../images/active_directory_threat_detection_lab_authentication_failures.png)

Wazuh displayed the authentication failures, allowing me to examine the associated Windows security events and their details. One of the events was Windows Security Event ID **4625**, which indicates that a logon attempt failed. Wazuh generated an alert using rule `60122`, classifying the event as a logon failure involving an unknown username or incorrect password.

## What did I learn from the investigation?

The most important part of this project wasn't simply seeing an alert appear. It was learning to examine the evidence behind it.

I reviewed details such as the account involved, the type of logon, the failure status, and the recorded source address. The event fields were consistent with an incorrect password.

The source address was `127.0.0.1`, also known as the loopback address. This is important because it does not identify a remote computer or an external attacker.

That distinction matters in security operations: **a security alert is a reason to investigate, not automatic proof of an attack.** Analysts need to interpret the available evidence, consider alternative explanations, and seek additional context before drawing conclusions.

## Why this matters for SOC analysis

This lab gave me hands-on experience with several activities relevant to a Security Operations Center (SOC):

- Reviewing endpoint authentication events in a SIEM.
- Identifying and examining a Windows security event.
- Interpreting alert fields and authentication failure codes.
- Distinguishing observed facts from assumptions.
- Documenting findings and identifying appropriate follow-up steps.

In a production environment, I would also review surrounding authentication activity and relevant domain-controller logs before deciding whether escalation was warranted.

## Final thoughts

This project helped me understand the practical workflow behind security event investigation: monitor, detect, examine, interpret, and document.

It also reinforced an important lesson: effective threat detection isn't just about generating alerts. It's about understanding what the evidence actually tells you.

**Explore the full project, including the lab architecture, screenshots, and technical investigation report:**

[View the Active Directory Threat Detection Lab on GitHub](https://github.com/Sviatko124/active-directory-threat-detection-lab)

I'm continuing to build my practical cybersecurity skills and develop projects that reflect the work involved in security monitoring and SOC analysis.
