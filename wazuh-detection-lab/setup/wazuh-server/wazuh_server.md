#  Wazuh Server Setup (Ubuntu)

This document outlines the steps to install and configure the **Wazuh Server** on an Ubuntu VM. The server includes the Wazuh manager, Elasticsearch, Filebeat, and the Wazuh dashboard.

---

##  Prerequisites

- **Operating System:** Ubuntu 20.04 or 22.04 (recommended)
- **Minimum Specs:** 2 vCPU, 4 GB RAM, 20 GB disk
- **Internet access required**

---

##  Step 1: Download and Run Wazuh Installer

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
chmod +x wazuh-install.sh
sudo bash ./wazuh-install.sh -a
```

> The `-a` flag installs the all-in-one Wazuh stack: manager, dashboard, and indexing components.

---

##  Step 2: Verify Services

After installation, ensure Wazuh components are running:

```bash
sudo systemctl status wazuh-manager
sudo systemctl status filebeat
sudo systemctl status elasticsearch
sudo systemctl status kibana
```

---

##  Step 3: Access the Wazuh Dashboard

1. Open a browser and go to:

   ```
   https://<your-server-ip>
   ```

2. Login credentials:

   - **Username:** admin
   - **Password:** admin

3. If using VirtualBox NAT or Host-Only, ensure port forwarding or bridge networking is enabled.

---

##  Step 4: Open Firewall (Optional)

If using `ufw`:

```bash
sudo ufw allow 443/tcp
```

---

##  Step 5: Confirm Web UI and Health

Once logged into the dashboard:

- Go to **"Management → Agents"**
- Confirm that the Wazuh Manager (localhost) appears
- Check module status: all should show green 

---

##  Screenshots 

| Description          | File                              |
| -------------------- | --------------------------------- |
| Dashboard Login Page | `screenshots/wazuh-login.png`     |
| Dashboard Home       | `screenshots/wazuh-dashboard.png` |
| System Health        | `screenshots/wazuh-health.png`    |

---

##  Optional Cleanup

If needed, uninstall:

```bash
sudo /var/ossec/uninstall.sh
```

---

##  Resources

- [Official Wazuh Install Docs](https://documentation.wazuh.com/current/installation-guide/installing-wazuh-server/index.html)
- [Troubleshooting](https://documentation.wazuh.com/current/installation-guide/installing-wazuh-server/troubleshooting.html)

---

>  Continue with: [setup/wazuh-agent.md](./wazuh-agent.md) to add a Windows machine as an agent.

