
# Sysmon Logs in Wazuh Dashboard

## Overview

Sysmon (System Monitor) is a powerful Windows system service that logs detailed events such as process creations, network connections, file changes, and more. When installed on a Windows agent machine, Sysmon generates rich event logs that Wazuh agents can collect and forward to the Wazuh manager for analysis and detection.

This document explains how Sysmon logs are collected by Wazuh and how to verify their presence and detections in the Wazuh dashboard.

---

## How Sysmon Integrates with Wazuh

1. **Sysmon** runs on the Windows agent and records events to the Windows Event Log (under "Microsoft-Windows-Sysmon/Operational").
2. The **Wazuh agent** on the Windows machine is configured to monitor these event channels.
3. Sysmon logs are forwarded by the Wazuh agent to the **Wazuh manager** (server).
4. The Wazuh manager analyzes the logs using predefined detection rules.
5. Alerts and events derived from Sysmon logs appear on the **Wazuh dashboard** under the corresponding agent.

---

## Verifying Sysmon Logs in Wazuh Dashboard

### 1. Access Wazuh Dashboard

Open your Wazuh web interface and navigate to the **"Security Events"** or **"Alerts"** section.

### 2. Filter by Agent

Select your Windows agent (e.g., `windowsagent1`) from the list of agents to focus on its events.

### 3. Identify Sysmon-Related Alerts

Look for alerts related to:

- Process creations initiated by PowerShell, `cmd.exe`, or suspicious binaries.
- Network connections initiated by unusual executables.
- Persistence or privilege escalation techniques (e.g., App Compatibility Database events).
- Discovery activities (e.g., `net.exe` commands).

These alerts are generated based on Sysmon’s detailed event data.

### 4. View Event Details

Click an alert to view detailed information, including:

- Event ID and description.
- Command lines executed.
- Parent and child process trees.
- MITRE ATT&CK tactic mappings.

---

## Example Alerts

| Timestamp           | Agent         | Alert Category        | Description                                            |
|---------------------|---------------|------------------------|--------------------------------------------------------|
| 2025-07-19 11:14:07 | windowsagent1 | Privilege Escalation   | Application Compatibility Database launched            |
| 2025-07-19 11:12:47 | windowsagent1 | Execution              | Suspicious binary `SecEdit.exe` launched by PowerShell |
| 2025-07-19 11:12:46 | windowsagent1 | Discovery              | Multiple `net.exe` account discovery commands          |

---

## Conclusion

Seeing these alerts in the Wazuh dashboard confirms:

- Sysmon is installed and running on the Windows agent.
- Wazuh agent is successfully collecting Sysmon event logs.
- Wazuh manager is analyzing and detecting suspicious activity from Sysmon data.

This integration provides rich visibility into Windows endpoint behavior for security monitoring.

---

## Screenshots

*Add screenshots of:*

- Wazuh dashboard alert list filtered by Windows agent.
- Expanded view of a Sysmon event alert.
- Sysmon configuration or installation confirmation on the agent VM.
