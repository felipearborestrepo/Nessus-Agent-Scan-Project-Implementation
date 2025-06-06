# Nessus Agent Scan Project Implementation

In this project, we demonstrate the deployment of a Nessus Agent on a Windows VM in Azure, and the configuration of an authenticated vulnerability scan using Tenable’s cloud platform.

_**Inception State:**_ No Nessus Agent installed or configured, no scan group created.

_**Completion State:**_ Nessus Agent fully installed, agent group created, scan run, vulnerabilities identified, and initial assessment conducted.

---

# Technology Utilized
- Tenable (Nessus Agent, Tenable.io Cloud platform)
- Azure Virtual Machines (Windows 10 Pro)
- PowerShell (Agent installation and configuration)
- Tenable Agent Groups (for grouping scan targets)

---

# Table of Contents

- [1. VM and Nessus Agent Setup](#1-vm-and-nessus-agent-setup)
- [2. Nessus Agent Group Creation](#2-nessus-agent-group-creation)
- [3. Agent Registration and Linking](#3-agent-registration-and-linking)
- [4. Agent Trigger and Vulnerability Scan](#4-agent-trigger-and-vulnerability-scan)
- [5. Vulnerability Findings and Results](#5-vulnerability-findings-and-results)
- [6. Final Summary](#6-final-summary)
- [7. Next Steps](#7-next-steps)

---

## 1. VM and Nessus Agent Setup

We start by provisioning a **Windows 10 Pro** virtual machine on Azure:

![VM Provisioned](https://github.com/user-attachments/assets/1-Created-VM.png)

Once provisioned, we downloaded and executed the PowerShell script to install the Nessus Agent and link it to Tenable.io:

```powershell
Invoke-WebRequest -Uri "https://sensor.cloud.tenable.com/install/agent/installer/ms-install-script.ps1" -OutFile "./ms-install-script.ps1"; & "./ms-install-script.ps1" -key "YOUR-KEY-HERE" -type "agent" -name "LABUSER-Agent-Group" -groups "LABUSER-Agent-Group"; Remove-Item -Path "./ms-install-script.ps1"
This installed and configured the Nessus Agent:

![Nessus Agent Installation](https://github.com/user-attachments/assets/9- Inside VM ran code in Powershell to Install the Agent.PNG)

The agent was successfully linked to sensor.cloud.tenable.com.

2. Nessus Agent Group Creation
In Tenable.io, we created a new Agent Group called LABUSER-Agent-Group to logically organize the agent(s):

![Agent Group Creation](https://github.com/user-attachments/assets/4- Added an Agent Group.png)

3. Agent Registration and Linking
In the Tenable.io portal, we confirmed the linked agent’s health and registration:

![Linked Agents](https://github.com/user-attachments/assets/8- Get Command from Linked Agents from Creating a new agent to run in the VM to install the Agent.png)

We verified the agent group membership and health status:

![Linked Agent Verification](https://github.com/user-attachments/assets/12- Made sure the Tenable Nessus Agent was running.PNG)

4. Agent Trigger and Vulnerability Scan
Trigger File Creation
On the VM, we navigated to the Nessus Agent triggers folder:

powershell
Copy
Edit
cd \
cd programdata
cd Tenable
cd 'Nessus Agent'
cd nessus
cd triggers
New-Item -Name star.txt
This star.txt file triggers the Nessus Agent to start a scan:

![Trigger File Created](https://github.com/user-attachments/assets/10- Created the star.txt file to trigger the scan.PNG)

After 10 minutes, the file was automatically deleted by the agent, indicating the scan had been triggered:

![File Deleted Automatically](https://github.com/user-attachments/assets/13- After 10 minutes the the file was deleted.PNG)

5. Vulnerability Findings and Results
We observed that the scan ran successfully and appeared in the Tenable.io Scans interface:

![Scan Triggered](https://github.com/user-attachments/assets/14- In Scans is showing as triggered.png)

Vulnerabilities were identified:

0 Critical

5 Medium

No Low vulnerabilities

![Vulnerability Details](https://github.com/user-attachments/assets/15- Check the Results from Scan.png)

A detailed list of vulnerabilities by plugin was also available:

![Vulnerabilities by Plugin](https://github.com/user-attachments/assets/15- Check the Results from Scan.png)

6. Final Summary
This installed and configured the Nessus Agent:

![Nessus Agent Installation](https://github.com/user-attachments/assets/9- Inside VM ran code in Powershell to Install the Agent.PNG)

The agent was successfully linked to sensor.cloud.tenable.com.

7. Next Steps
Incorporate the agent group into scheduled scans for ongoing vulnerability management.

Implement a remediation plan for the vulnerabilities discovered during the scan.

Explore automated integrations for asset health monitoring.

✅ Successfully deployed and registered the Nessus Agent on the Windows VM.
✅ Created an Agent Group in Tenable.io for scan management.
✅ Confirmed the agent’s operational status and triggered a scan via the star.txt method.
✅ Observed vulnerability findings in the Tenable.io console.
✅ The process established a foundation for continuous vulnerability management using Nessus Agents.

This project demonstrates a straightforward way to leverage Tenable’s agent-based scanning to monitor and secure cloud-based assets in an automated and controlled manner.

