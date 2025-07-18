# Attack Simulation #2: Suspicious File Creation

## Overview

This simulation demonstrates how attackers might drop malicious executables in publicly accessible locations like `C:\Users\Public`. This technique is often used for persistence or staging payloads, and Sysmon with Wazuh can detect such activity based on file creation events.

---

## Objective

To simulate a suspicious file creation event that triggers a Wazuh alert, validating detection of unauthorized file drops in a shared or system-critical location.

---

## Tools Used

- **PowerShell** (Built-in)
- **Sysmon** (for logging file creation)
- **Wazuh agent** (collecting event logs)
- **Wazuh manager/dashboard** (generating alert)

---

## Attack Steps

###  1. Run the Simulation (Windows Agent)

Open PowerShell as administrator and execute the following command:

```powershell
New-Item -Path "C:\Users\Public\malware-test.exe" -ItemType File
```

This command creates a dummy `.exe` file in the `Public` folder — a suspicious action from a monitoring standpoint.

---

## Expected Detection

Within a few seconds to minutes, Wazuh should raise an alert similar to the following:

| Field           | Value                                        |
|----------------|----------------------------------------------|
| **Agent**       | `windowsagent1`                              |
| **Timestamp**   | `Jul 19, 2025 @ 14:30:38`                    |
| **Category**    | Command and Control                          |
| **Description** | Executable file dropped in Users\Public folder |
| **Level**       | 12                                           |

This is based on **Sysmon Event ID 11**: File Create events.

---

## Screenshot

 Suggested file name:  
**`sim3-file-drop-alert-wazuh-dashboard.png`**

*Insert your screenshot showing the alert in the Wazuh dashboard here.*

---

## Conclusion

This simulation confirms that:
- Wazuh correctly detects suspicious file drops.
- Sysmon is actively monitoring file creation events.
- Public folders are being watched for possible misuse.

This activity mimics real-world attacker behavior and demonstrates that your logging and detection pipeline is functioning properly.

---

## MITRE ATT&CK Mapping

- **T1105** — Ingress Tool Transfer
- **T1059** — Command and Scripting Interpreter (PowerShell)