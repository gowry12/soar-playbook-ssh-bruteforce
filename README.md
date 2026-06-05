# SSH Brute-Force Detection and Automated Response using Wazuh and Shuffle SOAR

## Overview

This project demonstrates an automated Security Operations Center (SOC) workflow for detecting SSH brute-force attacks using Wazuh SIEM and responding through Shuffle SOAR automation.

The workflow enriches alerts with VirusTotal threat intelligence and notifies security analysts when malicious activity is detected, reducing manual investigation effort and improving response efficiency.

---

## Architecture

![SOAR Architecture](SOAR%20architecture.png)

The architecture follows a SIEM-to-SOAR workflow:

1. Wazuh detects SSH brute-force activity.
2. Alerts are forwarded to Shuffle SOAR using webhook integration.
3. Shuffle extracts the source IP address.
4. VirusTotal performs threat intelligence enrichment.
5. Decision logic determines whether the IP is malicious.
6. Email notification is sent to the SOC analyst when required.

---

## Technologies Used

| Tool              | Purpose                             |
| ----------------- | ----------------------------------- |
| Wazuh             | XDR / SIEM Platform                 |
| Shuffle SOAR      | Security Automation & Orchestration |
| VirusTotal        | Threat Intelligence Enrichment      |
| Kali Linux        | Attack Simulation                   |
| Email Integration | Analyst Notification                |

---

## Detection Workflow

### SSH Brute-Force Detection

Wazuh correlation rules monitor authentication logs and generate alerts when multiple failed login attempts occur within a short period.

### Alert Forwarding

Detected alerts are forwarded to Shuffle SOAR through webhook integration in JSON format.

### Threat Intelligence Enrichment

Shuffle queries VirusTotal using the attacker IP address and evaluates the reputation score.

### Automated Response

Based on the enrichment results:

* Malicious IP → Email notification sent to analyst.
* Non-malicious IP → Event logged without notification.

---

## Testing and Validation

### Scenario 1 – SSH Brute-Force Attack

A brute-force SSH attack was simulated using Hydra from a Kali Linux system.

Results:

* Wazuh detected the attack successfully.
* Alert forwarded to Shuffle SOAR.
* VirusTotal enrichment completed successfully.

### Scenario 2 – Email Notification Validation

Since the testing was performed using a personal IP address, VirusTotal did not classify the IP as malicious.

To verify notification functionality, a simulated malicious result was used.

Results:

* Email notification generated successfully.
* Alert details delivered to analyst mailbox.

---

## Key Outcomes

* Automated SSH brute-force detection
* SIEM-to-SOAR integration
* VirusTotal threat intelligence enrichment
* Conditional alert processing
* Automated analyst notification
* Reduced false positives

---

## MITRE ATT&CK Mapping

| Technique ID | Technique                                     |
| ------------ | --------------------------------------------- |
| T1110        | Brute Force                                   |
| T1078        | Valid Accounts (Potential Follow-on Activity) |

---

## Future Enhancements

* Automated IP blocking
* ServiceNow integration
* Jira ticket creation
* Multi-source alert correlation
* Advanced response automation

---

## Project Report

Detailed technical documentation is included in:

**SOAR Playbook Report.pdf**

---

## Author

**Gowry N**

SOC Analyst | Cybersecurity Enthusiast
