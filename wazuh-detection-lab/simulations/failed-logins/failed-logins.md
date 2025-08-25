\# Attack #1: Brute-force Login Simulation



\## Overview



This simulation mimics a brute-force attack by generating multiple failed login attempts on the Windows agent. Wazuh should detect this activity and generate alerts related to authentication failures.



---



\## Simulation Steps



1\. \*\*On the Windows Agent VM\*\*, open PowerShell.

2\. Run the following command to simulate failed logins:



```powershell

for ($i=0; $i -lt 10; $i++) {

&nbsp;   net use \\\\localhost\\IPC$ /user:fakeuser wrongpassword

}

This will generate failed login attempts by trying to authenticate with invalid credentials.



#### 

#### Expected Wazuh Detection



Rule Name: Multiple failed authentication attempts



Alert Level: Medium to High



Category: Authentication, Brute Force



Source: Windows Security Logs → Event ID 4625 (failed logon)



#### Screenshots:

Wazuh Dashboard showing the alert.



Failed logon event details (Event ID 4625).



PowerShell script execution.





