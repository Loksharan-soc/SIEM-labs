\# Sysmon Installation Guide



\## Overview



Sysmon (System Monitor) is a Windows system service that logs detailed system activity such as process creation, network connections, and file time changes. These logs help detect suspicious behavior when monitored by Wazuh.



\## Installation Steps



\### 1. Download Sysmon



Download Sysmon from the official Microsoft Sysinternals website:  

https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon



\### 2. Download Sysmon Configuration File



Open PowerShell as Administrator and run the following command to download a community Sysmon config file:



```powershell

Invoke-WebRequest -Uri "https://raw.githubusercontent.com/SwiftOnSecurity/sysmon-config/master/sysmonconfig-export.xml" -OutFile "C:\\Users\\vboxuser1\\Downloads\\Sysmon\\sysmonconfig.xml"

```



\### 3. Install Sysmon with Config



Still in PowerShell, navigate to the Sysmon folder and install Sysmon using the config:



```powershell

cd C:\\Users\\vboxuser1\\Downloads\\Sysmon

.\\Sysmon64.exe -accepteula -i sysmonconfig.xml

```



You should see output like this:



```

Sysmon64 installed.

SysmonDrv installed.

Starting SysmonDrv.

SysmonDrv started.

Starting Sysmon64..

Sysmon64 started.

```



\## Verification



\### Check if Sysmon service is running:



```powershell

Get-Service sysmon64

```



\### View Sysmon logs in Event Viewer:



Open the Run dialog (Win + R), type `eventvwr.msc`, and press Enter.  

Navigate to:



```

Applications and Services Logs > Microsoft > Windows > Sysmon > Operational

```



You should now see Sysmon logs being generated.



---



\## Screenshots



\### Sysmon Files



!\[Sysmon folder](./screenshots/sysmon-folder-view.png)



\### Sysmon Installation Output



!\[Sysmon install](./screenshots/sysmon-install-command.png)



\### Sysmon Event Logs in Event Viewer



!\[Sysmon logs](./screenshots/sysmon-eventviewer-logs.png)









