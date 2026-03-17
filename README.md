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
