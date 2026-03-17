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

### 🖼️ Demo: 
[Watch Full Demo](https://drive.google.com/file/d/1HJznsLTW11QqCWwRigrPFWWUI_gj3wQs/view?usp=sharing)

---

## 🔴 Scenario 2: Lateral Movement via SSH Agent Hijacking

### 🧪 Attack
This scenario simulates **SSH Agent Hijacking**, where an attacker abuses **SSH Agent Forwarding (`ssh -A`)** to move laterally across the network.

In a typical workflow:
- A legitimate user connects from their local machine → Jump Box → internal servers (Server Farm)
- Authentication is handled via **SSH Agent Forwarding**, without re-entering credentials

However, this introduces a security risk:
- The forwarded agent is exposed via the `SSH_AUTH_SOCK` environment variable
- If the attacker compromises the Jump Box, they can:
  - Access `SSH_AUTH_SOCK`
  - Reuse the victim’s SSH agent
  - Authenticate to internal servers **without the private key**

---

### 🖥️ Environment Setup

| Machine | IP Address | User |
|--------|-----------|------|
| Jump Box | 192.168.49.140 | jumpbox |
| User Machine | 192.168.49.138 | nt1208 |
| Server Farm | 172.19.192.36 | server |

---

### 🔍 Detection
- Wazuh monitors SSH activities and session behavior
- Suspicious indicators:
  - SSH sessions initiated without normal authentication flow
  - Abuse of `SSH_AUTH_SOCK` environment variable
  - Unusual access pattern from Jump Box to internal servers
- Logs are analyzed to detect abnormal session reuse

---

### ⚡ Response
When malicious SSH usage is detected, **Active Response** is triggered:

- Terminate the active SSH session to the Server Farm
- Disable or lock the compromised `jumpbox` user
- Prevent further lateral movement
- Generate alert for SOC investigation

---

### 🖼️ Demo: 
[Watch Full Demo](https://drive.google.com/file/d/1Tfn4od8djykwGdD7UtQqqaeHDyJAMHyg/view?usp=sharing)
