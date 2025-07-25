# Splunk Enterprise Server Setup Guide

This document describes the step-by-step process to install and configure Splunk Enterprise as a server (indexer + search head) on an Ubuntu machine.

---

## Prerequisites

- Ubuntu 20.04 or later installed on the server machine  
- Minimum 4GB RAM, 2 CPU cores  
- At least 20GB free disk space  
- User with sudo privileges  
- Internet connectivity to download Splunk packages  

---

## Step 1: Download Splunk Enterprise

1. Visit the official Splunk download page:  
   https://www.splunk.com/en_us/download/splunk-enterprise.html

2. Select **Linux** platform and download the latest `.deb` package for Ubuntu/Debian.

Alternatively, from your Ubuntu server terminal run:

```bash
wget -O splunk.deb 'https://download.splunk.com/products/splunk/releases/9.1.0/linux/splunk-9.1.0-a7f645ddaf91-linux-2.6-amd64.deb'
```

*(Replace the URL with the latest version link.)*

---

## Step 2: Install Splunk Enterprise

Run the following commands:

```bash
sudo dpkg -i splunk.deb
```

If there are missing dependencies, run:

```bash
sudo apt-get install -f
```

---

## Step 3: Start and Enable Splunk

Start Splunk and accept the license:

```bash
sudo /opt/splunk/bin/splunk start --accept-license
```

You will be prompted to create the admin username and password.

Enable Splunk to start on boot:

```bash
sudo /opt/splunk/bin/splunk enable boot-start
```

---

## Step 4: Configure Firewall

Allow Splunk Web UI (default port 8000) and Splunk management port (default 8089):

```bash
sudo ufw allow 8000/tcp
sudo ufw allow 8089/tcp
sudo ufw reload
```

---

## Step 5: Access Splunk Web UI

Open a web browser and go to:

```
http://<your-server-ip>:8000
```

Log in with the admin credentials you set.

---

## Step 6: Initial Configuration

- Set the timezone and other preferences.
- Configure data inputs and indexes as per your needs.
