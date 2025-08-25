
# Splunk SIEM Lab

This project is a hands-on Security Information and Event Management (SIEM) lab built using Splunk Enterprise. It simulates real-world cyber attacks and detects them using custom SPL queries, dashboards, and MITRE ATT&CK mappings. The goal is to demonstrate threat detection, log analysis, and SOC-style alerting capabilities in a controlled lab environment.

---

## Lab Setup

- Splunk Enterprise (All-in-one) installed on an Ubuntu VM  
- Splunk Universal Forwarder deployed on a Windows 10 VM  
- Log Sources:
  - Windows Security Event Logs
  - PowerShell logs
  - Sysmon (with SwiftOnSecurity config)

> All machines are virtualized and isolated in a home lab environment.

---

## Simulated Attacks

| Attack               | Description                                  | MITRE Technique             |
|----------------------|----------------------------------------------|-----------------------------|
| Brute-force login    | Multiple failed RDP logins                    | T1110 – Brute Force          |
| PowerShell Malware    | Malicious PowerShell execution via encoded script | T1059.001 – PowerShell      |
| Suspicious File Drop  | Executable dropped in `C:\Users\Public`       | T1105 – Ingress Tool Transfer |
| Registry Persistence  | Registry key modified for persistence          | T1547.001 – Registry Run Keys |

---

## Detection & Dashboards

- SPL Queries to detect each attack scenario  
- Dashboards built to visualize attack patterns  
- Custom alerts (manual or scheduled) for threat visibility

See the `detections/` and `dashboards/` folders for full details.

---

## Repo Structure

```
splunk-siem-lab/
├── setup/                 # Splunk & forwarder setup guides
├── simulations/           # Attack walkthroughs
├── detections/            # SPL queries + MITRE mapping
├── dashboards/            # Dashboards and screenshots
├── screenshots/           # UI screenshots used in markdown
└── README.md              # This file
```

---

## Goals

- Demonstrate hands-on experience with Splunk as a SIEM tool  
- Build detection logic mapped to MITRE ATT&CK  
- Prepare for cybersecurity internship interviews and technical screening

---

## Skills Demonstrated

- Splunk installation & configuration  
- Log ingestion and forwarder setup  
- Threat detection using SPL  
- SIEM dashboards and alerting  
- Red vs Blue lab simulations  
- MITRE ATT&CK mapping

---

## Author

**Loksharan Saravanan**  
Jersey City, NJ  
[linkedin.com/in/loksharan](https://linkedin.com/in/loksharan)  
[github.com/loksharan-soc](https://github.com/loksharan-soc)
