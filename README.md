# 🛡️ Researching and Implementing a Unified Endpoint Protection Platform

## 👥 Contributors
| MSSV | Contributor | Full Name |
|:--------|:-------------|:-----------------------|
| 21522312 | luongpd2313 | Phùng Đức Lương |
| 21522620 | nt1208 | Hồ Ngọc Thiện |

---

## 📌 Overview
This project implements a **Next-Generation Endpoint Protection Platform (NG-EPP)** using open-source tools.

The system integrates multiple security layers into a unified platform:
- SIEM & EDR (Wazuh)
- Antivirus (ClamAV)
- Firewall (iptables)
- Device Control (USBGuard)
- Vulnerability Management
- AI-powered Threat Hunting (RAG)

The goal is to simulate a **real-world SOC environment**, where attacks are detected, analyzed, and responded to in real time.

---

## 🧱 Core Components

- **Wazuh**: SIEM + EDR (log collection, detection, response)
- **ClamAV**: Malware detection
- **iptables**: Network-level protection
- **USBGuard**: Device control
- **MongoDB + Flask**: Data processing for vulnerability module
- **AI (RAG + LLM)**:
  - Log analysis
  - Threat explanation
  - Remediation suggestions

---
# 🚨 Attack Scenarios & Demonstration

---

## 🔴 Scenario 1: Reverse Shell Detection & Response

### 🧪 Attack
A malicious Python script simulating a **reverse shell** is executed on the endpoint.  
The script initiates an outbound connection to the attacker's machine, allowing remote command execution and persistent access.

---

### 🔍 Detection
- The `lsof-monitor` service detects new outbound network connections.
- Logs are forwarded by **Wazuh Agent** to the **Wazuh Manager**.
- Wazuh analyzes:
  - Destination IP address
  - Process information (PID, command line, user)
- The connection is compared against a **blacklist of suspicious IPs**.
- An alert is generated when a match or abnormal behavior is detected.

---

### ⚡ Response
Once the alert is triggered, **Active Response** is executed automatically:

- Analyze the suspicious process (PID, command line, user)
- Check if the process originated from a USB device  
  → If yes, block the device using USB control
- Terminate the reverse shell process
- Delete the malicious file from the system
- Isolate the endpoint from the network for further investigation

---

### 🖼️ Demo

**1. Reverse shell execution**
```md
[Watch Full Demo](https://drive.google.com/file/d/1HJznsLTW11QqCWwRigrPFWWUI_gj3wQs/view?usp=sharing)
```
