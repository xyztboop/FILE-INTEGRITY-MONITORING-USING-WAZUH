# FILE-INTEGRITY-MONITORING-USING-WAZUH

Objective

✔️ Implement FIM on a monitored machine

✔️ Detect file creation, deletion, or modification

✔️ Configure Wazuh Server and Agent to communicate securely

✔️ Visualize alerts in Wazuh Dashboard

✔️ Simulate unauthorized changes and verify alert generation

What is File Integrity Monitoring?

File Integrity Monitoring is a security process that:

✔ Compares current file metadata to a trusted baseline

✔ Detects unauthorized changes to files and directories

✔ Helps identify security breaches or policy violations

FIM is commonly used in enterprise environments and is required by compliance standards such as ISO 27001 and PCI-DSS.

TOOLS USED FOR PROJECT:

| Tool                      | Purpose                               |
| ------------------------- | ------------------------------------- |
| Ubuntu                    | Operating system for Server/Agent     |
| Wazuh Server              | Collects, analyzes, and stores alerts |
| Wazuh Agent               | Installed on monitored machine        |
| Wazuh Dashboard           | GUI to view alerts & events           |
| Virtualization (optional) | VMware/VirtualBox for labs            |

ARCHITECTURE:
Monitored Machine → Wazuh Agent → Filebeat - Wazuh Manager → Dashboard

Deployment Steps

 1. Setup Wazuh Server

Install Wazuh Server on Ubuntu

Install and configure Wazuh Dashboard

Ensure your server can communicate with Wazuh agents

The server collects alerts from all connected endpoints and displays them in the Dashboard.

2. Configure Wazuh Agent for FIM

On the agent machine (Ubuntu):

Open the agent config:

sudo nano /var/ossec/etc/ossec.conf

<syscheck>
  <frequency>600</frequency>
  <directories check_all="yes" report_changes="yes" realtime="yes">/home/username</directories>
</syscheck> 

<img width="602" height="184" alt="image" src="https://github.com/user-attachments/assets/7459fbdc-9a10-405f-a602-b970e2b9341c" />

This monitors changes in the Public Documents folder.

<img width="602" height="358" alt="image" src="https://github.com/user-attachments/assets/d00d2fc1-ad20-45c6-a385-267ca1257013" />

Restart Wazuh Manager to apply changes
sudo systemctl restart wazuh-manager

<img width="645" height="81" alt="image" src="https://github.com/user-attachments/assets/ab4c480a-b662-4106-b2a5-3f0dc3f83af7" />

Testing the Project

To verify FIM is working:

Create a test file:

sudo touch var/www/testfile.txt

<img width="431" height="57" alt="image" src="https://github.com/user-attachments/assets/5ef7febb-ff07-4e6c-8285-6e5a267daac0" />

Add some content:

 sudo nano /var/www/testfile.txt
 
 <img width="449" height="54" alt="image" src="https://github.com/user-attachments/assets/437b7de5-af03-487a-b9a6-127e90a21f70" />


Delete the file:

sudo rm /var/www/testfile.txt

<img width="362" height="56" alt="image" src="https://github.com/user-attachments/assets/632e2f5a-2b6c-458c-93a4-9712130ff677" />

If FIM is configured correctly, events will appear under Security Events → FIM in the Wazuh Dashboard.
Dashboard Output & Alert Analysis

<img width="602" height="294" alt="image" src="https://github.com/user-attachments/assets/bbb568ee-8ec5-471e-816c-774ec81db611" />

Agent Status:

Agent Name: kali

Status: Active

IP Address: 192.168.56.105

Version: Wazuh v4.7.5

OS: Kali GNU/Linux

This confirms the monitored endpoint is successfully connected to the Wazuh manager.
FIM Recent Events (From Dashboard)

The following file integrity events were detected:

File Path	Action	Rule ID	Description
/root/www/testfile.txt	Deleted	553	File deleted
/root/www/testfile.txt	Modified	550	Integrity checksum changed
/root/www/testfile.txt	Modified	550	Integrity checksum changed

What This Means

When the file was modified → Wazuh detected a hash change

When the file was deleted → Wazuh triggered a file deletion alert

Each event generated a rule-based alert inside the dashboard

<img width="1893" height="902" alt="image" src="https://github.com/user-attachments/assets/9ed6f94e-d6fa-4a91-b12f-ad0c99587f3b" />

<img width="1859" height="663" alt="Screenshot 2026-02-22 151740" src="https://github.com/user-attachments/assets/c782566d-0edf-4565-841a-383d7f4d09a5" />
Conclusion:
This project helped me implement file integrity monitoring using Wazuh to detect and analyze unauthorized file changes.It demonstrates real world skills used in IT technologies and SOC centers and Incident response.



