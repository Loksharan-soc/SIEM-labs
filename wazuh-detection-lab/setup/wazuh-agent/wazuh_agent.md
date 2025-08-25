#  Wazuh Agent Setup (Windows)

This document outlines how to install and connect the **Wazuh Agent** on a Windows machine to your Wazuh Server.

---

##  Prerequisites

- **Windows Version:** Windows 10 or 11 (x64)
- Wazuh Server must be installed and accessible
- Windows VM must be on the same network as the Wazuh Server

---

## 🔧 Step 1: Download Wazuh Agent for Windows

1. Visit: [https://packages.wazuh.com/4.x/windows/wazuh-agent-4.7.0-1.msi](https://packages.wazuh.com/4.x/windows/wazuh-agent-4.7.0-1.msi)
2. Save the `.msi` installer on the Windows VM

---

##  Step 2: Install the Agent

Double-click the `.msi` file to launch the installation wizard:

- Click **Next** until you reach the **Configuration** screen
- Enter your Wazuh Server IP (Ubuntu VM) as the **Manager IP**
- Keep default settings unless otherwise needed

---

##  Step 3: Register and Start the Agent

After installation, register the agent manually using PowerShell (as Administrator):

```powershell
"C:\Program Files (x86)\ossec-agent\agent-auth.exe" -m <WAZUH_SERVER_IP>
```

Then start the agent:

```powershell
Restart-Service -Name wazuh
```

---

##  Step 4: Confirm Agent is Connected

1. Log in to the **Wazuh Dashboard**: `https://<your-server-ip>`
2. Go to **Management → Agents**
3. Look for the Windows agent in the list
4. Status should show as **Active**

---

##  Screenshots 

| Description          | File                              |
| -------------------- | --------------------------------- |
| Agent Install Wizard | `screenshots/agent-install.png`   |
| Agent Auth Command   | `screenshots/agent-auth.png`      |
| Agent Active in UI   | `screenshots/agent-connected.png` |

---

##  Optional: Uninstall Agent

To remove the agent:

- Go to **Control Panel → Programs → Uninstall a program**
- Find and uninstall **Wazuh Agent**

Or use PowerShell:

```powershell
Get-WmiObject -Class Win32_Product | Where-Object { $_.Name -like "*Wazuh*" } | ForEach-Object { $_.Uninstall() }
```

---

##  Resources

- [Wazuh Agent Docs](https://documentation.wazuh.com/current/installation-guide/installing-wazuh-agent/win-wazuh-agent.html)
- [Agent Auth](https://documentation.wazuh.com/current/user-manual/agent-auth/index.html)

---

>  Continue with: [../simulations/](../simulations/) to simulate an attack and detect it with Wazuh.

