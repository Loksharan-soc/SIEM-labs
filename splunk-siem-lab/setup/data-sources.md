\# Data Sources



This document lists the log sources ingested into the Splunk SIEM lab environment from the Windows Universal Forwarder. These data sources provide visibility into system, security, and application activity, helping detect suspicious or malicious behavior.



\## Configured Log Sources (via `inputs.conf`)



The configuration file `inputs.conf` is located at:



```

C:\\Program Files\\SplunkUniversalForwarder\\etc\\system\\local\\inputs.conf

```



It contains the following configuration:



```ini

\[WinEventLog://Security]

disabled = 0

index = main



\[WinEventLog://System]

disabled = 0

index = main



\[WinEventLog://Application]

disabled = 0

index = main



\[WinEventLog://Microsoft-Windows-Sysmon/Operational]

disabled = 0

index = main

```



These stanzas enable collection of:



\- \*\*Security Log\*\*: Logon attempts, privilege use, and other audit events

\- \*\*System Log\*\*: Driver/Service issues, shutdowns, and system-level errors

\- \*\*Application Log\*\*: Application errors and messages

\- \*\*Sysmon Operational Log\*\*: Detailed process creation, network connections, registry changes, etc. (Requires Sysmon to be installed and configured)



---



\## Configured Log Sources



\### 1. Windows Event Logs



| Log Name        | Description                                     | Sourcetype                 | Notes                                      |

|-----------------|------------------------------------------------|----------------------------|--------------------------------------------|

| Security        | Security events such as logins, logouts, user activity | WinEventLog:Security       | Critical for detecting unauthorized access |

| System          | System-level events like driver or service failures | WinEventLog:System         | Useful for system health and anomalies     |

| Application     | Application logs including errors and warnings  | WinEventLog:Application    | Helps track application crashes or issues  |



\### 2. Sysmon Logs



| Log Name                    | Description                              | Sourcetype                       | Notes                                               |

|-----------------------------|----------------------------------------|---------------------------------|-----------------------------------------------------|

| Microsoft-Windows-Sysmon/Operational | Detailed monitoring of process creation, network connections, file creations, and more | WinEventLog:Microsoft-Windows-Sysmon/Operational | Provides granular visibility into system activity; highly recommended for threat detection |



---



\## Optional Additional Sources (Not currently enabled)



These can be added to increase monitoring coverage:



| Log Name                                      | Description                               | Suggested Sourcetype                         |

|-----------------------------------------------|-------------------------------------------|----------------------------------------------|

| Windows PowerShell                            | Logs PowerShell command execution         | WinEventLog:Windows PowerShell               |

| Microsoft-Windows-TaskScheduler/Operational  | Logs scheduled task creation and execution | WinEventLog:Microsoft-Windows-TaskScheduler/Operational |

| Microsoft-Windows-WMI-Activity/Operational   | Logs WMI activity                          | WinEventLog:Microsoft-Windows-WMI-Activity/Operational |

| Security logs from other critical Windows components (e.g., DNS Server, Firewall) | Depending on use case | Varies                                       |



---



\## Summary



The current Splunk Universal Forwarder configuration collects logs primarily from the standard Windows Event Logs (Security, System, Application) and Sysmon (if installed). These sources form the foundation for security monitoring and incident detection.



Additional sources may be added based on the environment and detection needs.



---



\## References



\- \[Splunk Inputs for Windows](https://docs.splunk.com/Documentation/Splunk/latest/Data/MonitorWindowsEventLogs)

\- \[Sysmon Guide](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon)

\- \[Windows Security Event IDs](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/)





