# Windows PowerShell Monitoring Using Wazuh

## 📌 Project Overview

This project demonstrates how to monitor Windows PowerShell activity using **Wazuh SIEM**.

I enabled PowerShell Script Block Logging and configured the Wazuh agent to collect PowerShell events from Windows Event Viewer.

The main objective was to understand how SOC Analysts monitor PowerShell activity and investigate suspicious commands.

## 🎯 Objectives

- Enable PowerShell Script Block Logging.
- Monitor Windows Event ID 4104.
- Collect PowerShell logs using the Wazuh agent.
- Detect suspicious PowerShell-related activity.
- Investigate alerts using the Wazuh Dashboard.
- Understand MITRE ATT&CK techniques.

## 🛠️ Tools Used

- Wazuh SIEM 4.14.9
- Windows 11
- Ubuntu Linux
- VirtualBox
- Windows PowerShell
- Wazuh Dashboard

## ⚙️ Lab Configuration

### Step 1: Enable PowerShell Script Block Logging

Enabled Script Block Logging through the Windows Registry.

Registry path:

`HKLM\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging`

Configured:

`EnableScriptBlockLogging = 1`

### Step 2: Configure Wazuh Agent

Added the following configuration to the Wazuh agent's `ossec.conf` file:

```xml
<localfile>
  <location>Microsoft-Windows-PowerShell/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
```

Restarted the Wazuh agent after configuration.

### Step 3: Monitor PowerShell Events

Monitored the following Windows Event ID:

- **4104** – PowerShell Script Block Logging

Verified that PowerShell events were forwarded to the Wazuh manager.

### Step 4: Investigate Wazuh Alerts

Searched for Rule ID `91843` in the Wazuh Dashboard.

Observed an alert related to PowerShell registry modification activity.

## 🔍 Detection Results

| Field | Observed Result |
|---|---|
| Event ID | 4104 |
| Wazuh Rule ID | 91843 |
| Alert Level | 3 |
| Decoder | windows_eventchannel |
| MITRE Technique | T1059.001 |
| MITRE Technique | T1112 |

**MITRE ATT&CK Mapping:**

- T1059.001 – PowerShell
- T1112 – Modify Registry

The observed registry modification was generated intentionally during lab configuration. It was not evidence of a real attack.

## 📚 What I Learned

- How PowerShell Script Block Logging works.
- How to monitor Event ID 4104.
- How Wazuh collects Windows Event Channel logs.
- How to investigate PowerShell alerts.
- How to understand MITRE ATT&CK mappings.
- How SOC Analysts monitor suspicious command execution.

## 🏁 Project Status

**Completed – Day 10 of my SOC Analyst Home Lab Journey.**

This hands-on project helped me improve my practical knowledge of Windows Security Monitoring and SIEM investigation.

