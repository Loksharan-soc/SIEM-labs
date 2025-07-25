
# Splunk Universal Forwarder Agent Setup on Windows VM

## Overview
This document guides you through installing and configuring the Splunk Universal Forwarder on a Windows VM to forward logs to a Splunk Enterprise server.

---

## Prerequisites
- Windows VM running with Administrator access.
- Splunk Enterprise server IP address and receiving port (default: 9997).
- Valid Splunk admin username and password.

---

## Step 1: Download Splunk Universal Forwarder for Windows
1. Visit the official Splunk download page: https://www.splunk.com/en_us/download/universal-forwarder.html
2. Select Windows and download the latest Universal Forwarder `.msi` installer.

---

## Step 2: Install Splunk Universal Forwarder
1. Run the installer `.msi` as Administrator.
2. Follow the prompts and accept the license agreement.
3. Choose default installation path or customize as needed.
4. When prompted, **do not** configure the deployment server now (leave blank).
5. Finish the installation.

---

## Step 3: Open PowerShell as Administrator
1. Search for PowerShell, right-click, and select **Run as administrator**.

---

## Step 4: Navigate to the Splunk Universal Forwarder `bin` directory
```powershell
cd "C:\Program Files\SplunkUniversalForwarder\bin"
```

---

## Step 5: Configure the forward server (Splunk Enterprise server)
Replace `<Splunk_Server_IP>` with your Splunk Enterprise server IP, and use port `9997` by default:
```powershell
.\splunk.exe add forward-server <Splunk_Server_IP>:9997 -auth admin:<password>
```

Example:
```powershell
.\splunk.exe add forward-server 192.168.1.157:9997 -auth admin:password123
```

---

## Step 6: Add log monitors
Add the Windows Event Logs you want to forward:

```powershell
.\splunk.exe add monitor "C:\Windows\System32\winevt\Logs\Security.evtx" -sourcetype WinEventLog:Security -index main -auth admin:<password>

.\splunk.exe add monitor "C:\Windows\System32\winevt\Logs\Application.evtx" -sourcetype WinEventLog:Application -index main -auth admin:<password>

.\splunk.exe add monitor "C:\Windows\System32\winevt\Logs\System.evtx" -sourcetype WinEventLog:System -index main -auth admin:<password>
```

---

## Step 7: Restart the Splunk Forwarder
```powershell
.\splunk.exe restart
```

---

## Step 8: Verify forwarding status
To check if the forward server is active:
```powershell
.\splunk.exe list forward-server
```

You should see your Splunk Enterprise server IP listed as active.

---

## Step 9: Confirm data in Splunk Enterprise
1. Log in to your Splunk Web UI (e.g., http://<Splunk_Server_IP>:8000).
2. Run a search query to verify incoming data:
```
index=main sourcetype="WinEventLog:Security"
```
