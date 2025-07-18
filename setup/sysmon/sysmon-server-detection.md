# Sysmon Server-Side Detection with Wazuh

## Overview

This document explains how to verify that Sysmon logs generated on the Windows agent are successfully received and parsed by the Wazuh server. This completes the end-to-end detection pipeline using Sysmon for logging and Wazuh for detection and alerting.

---

## 1. Confirm Sysmon Logs Are Received on Wazuh Server

Run the following command on the **Ubuntu Wazuh server** to view live log collection activity:

```bash
sudo tail -f /var/ossec/logs/ossec.log
```

Now, generate an event on the **Windows VM** (like opening `cmd.exe`, or launching a browser). Look for lines in the Wazuh log like:

```
ossec-logcollector: INFO: (1950): Analyzing event log: 'Microsoft-Windows-Sysmon/Operational'
```

This confirms that the Wazuh agent is collecting Sysmon logs from the Windows event channel.

---

## 2. View Sysmon Events in Wazuh Dashboard

To confirm the logs are being parsed and alerts are generated:

1. Open the Wazuh Dashboard in your browser:  
   `https://<your-wazuh-server-ip>:5601`

2. Navigate to:  
   **Security Events** → Select your Windows agent

3. Use this filter in the search bar to isolate Sysmon-related events:
   ```
   rule.groups: "windows" AND data.win.system.provider_name: "Microsoft-Windows-Sysmon"
   ```

4. You should see events like:
   - Event ID 1: Process Creation
   - Event ID 3: Network Connection
   - Event ID 11: File Creation
   - Event ID 13: Registry Modifications

---

## 3. Enable or Update Sysmon Detection Rules (Optional)

If you're not seeing Sysmon alerts, update your Wazuh ruleset with the latest Sysmon detection rules:

```bash
cd /var/ossec/etc/rules
sudo wget https://raw.githubusercontent.com/wazuh/wazuh/master/ruleset/rules/windows_sysmon_rules.xml
```

Then, include it in your main Wazuh config file:

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Make sure the following line exists:

```xml
<include>rules/windows_sysmon_rules.xml</include>
```

Restart the Wazuh manager:

```bash
sudo systemctl restart wazuh-manager
```

---

## 4. Example: Sysmon Alert in Dashboard

Below is an example of a Process Creation event detected by Wazuh via Sysmon:

![Sysmon alert in Wazuh dashboard](../screenshots/sysmon-alert-dashboard.png)

---

## Notes

- Sysmon logs on their own do not generate alerts — they must be monitored by a detection engine like Wazuh.
- You can customize or write additional rules to fine-tune detections (e.g., alert only on unsigned binaries or suspicious PowerShell use).
- This server-side validation is key to showing that your SOC pipeline works end-to-end.

---

## Next Steps

After verifying detection:
- Simulate basic attacks (PowerShell abuse, suspicious EXEs, registry changes)
- Document alerts and match them with Sysmon Event IDs
