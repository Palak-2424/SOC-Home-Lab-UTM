# SOC-Home-Lab-UTM-MacOS

> A fully virtualized, self-contained Security Operations Center (SOC) lab built using UTM on macOS. The lab simulates real-world attack and defense scenarios using Splunk (SIEM), Suricata (IDS), Nessus (vulnerability scanner), Sysmon (endpoint telemetry), and Splunk Universal Forwarder, distributed across three VMs.

---

## 📑 Table of Contents

* [Project Overview](#project-overview)
* [Architecture](#architecture)
* [Tools Used](#tools-used)
* [Virtual Machine Setup](#virtual-machine-setup)
* [Step-by-Step Lab Configuration](#step-by-step-lab-configuration)
* [Detection Use Cases](#detection-use-cases)
* [Screenshots](#screenshots)
* [Next Steps & Contributions](#next-steps--contributions)
* [License](#license)

---

## 🧠 Project Overview

This repository provides a structured environment for blue teamers and SOC analysts to build detection engineering skills. Built entirely within **UTM on macOS**, this lab simulates:

* Endpoint-level telemetry collection (via Sysmon)
* Network-level intrusion detection (via Suricata)
* Centralized log correlation and analysis (via Splunk)
* Vulnerability scanning and posture evaluation (via Nessus)
* Attack simulation (via Kali Linux)

---

## 🏗️ Architecture

**UTM Virtual Machines:**

* **Ubuntu Server**: Runs Splunk, Suricata IDS, and Nessus
* **Windows 10**: Configured with Sysmon and Splunk Universal Forwarder
* **Kali Linux**: Attacker simulation tools and payload generation

```text
+----------------+       +----------------+       +----------------+
|   Kali Linux   | <---> |   Windows 10   | <---> |    Ubuntu VM   |
| (Attacker VM)  |       |  (Victim VM)   |       | (SOC Services) |
+----------------+       +----------------+       +----------------+
```

All VMs are connected via an **internal virtual LAN** within UTM.

---

## 🛠️ Tools Used

| Tool              | Description                           |
| ----------------- | ------------------------------------- |
| Splunk Enterprise | SIEM and centralized log aggregator   |
| Suricata IDS      | Network intrusion detection system    |
| Nessus Essentials | Vulnerability scanning                |
| Sysmon            | Windows system event telemetry        |
| Splunk UF         | Log forwarder from endpoint to Splunk |
| Kali Linux Tools  | Nmap, Metasploit, Mimikatz, etc.      |
| UTM (macOS)       | Virtualization platform               |

---

## 🧰 Virtual Machine Setup

### 1. Ubuntu (SOC Server)

* OS: Ubuntu 22.04 LTS
* Tools: Splunk Enterprise, Suricata IDS, Nessus Essentials
* Purpose: Receives logs, detects attacks, scans vulnerabilities

### 2. Windows 10 (Victim)

* Tools: Sysmon (SwiftOnSecurity config), Splunk UF
* Purpose: Generates real-time endpoint telemetry

### 3. Kali Linux (Attacker)

* Tools: nmap, msfvenom, hydra, mimikatz, netcat
* Purpose: Simulates adversarial behavior against the Windows VM

---

## ⚙️ Step-by-Step Lab Configuration

### Step 1: Install UTM and Create VMs

* Install UTM from [https://mac.getutm.app/](https://mac.getutm.app/)
* Create 3 VMs: Ubuntu, Windows 10, Kali Linux
* Use **shared or host-only network mode** for isolated communication

### Step 2: Ubuntu VM Setup (Splunk + Suricata + Nessus)

* Install Splunk via `.deb` package → enable port 8000
* Configure inputs.conf to listen on `9997` for logs
* Install Suricata → Enable `eve.json` logging
* Register Nessus Essentials and perform local scans

### Step 3: Windows 10 Setup (Sysmon + Splunk UF)

* Install Sysmon using SwiftOnSecurity config
* Install Splunk Universal Forwarder
* Configure output to Ubuntu Splunk on port `9997`

### Step 4: Kali Linux Setup (Attack Simulations)

* Launch scans: `nmap`, `hydra`, `msfvenom`
* Use mimikatz for credential dumping
* Observe telemetry in Splunk + Suricata logs

---

## 🔍 Detection Use Cases

| Attack Scenario      | Detection Tool | Source  | Observable Event             |
| -------------------- | -------------- | ------- | ---------------------------- |
| Port scanning (nmap) | Suricata       | Ubuntu  | `ET SCAN Nmap` signature     |
| Credential dumping   | Sysmon         | Windows | Event ID 10: LSASS access    |
| Reverse shell        | Suricata       | Ubuntu  | Suspicious outbound TCP flow |
| Nessus scan          | Splunk         | Ubuntu  | Unusual port probes          |

---

## 📸 Screenshots

Please upload all screenshots to the `screenshots/` folder.
Examples:

* `screenshots/splunk-sysmon.png`
* `screenshots/suricata-nmap-detect.png`
* `screenshots/nessus-report.png`

---

## 🚀 Next Steps & Contributions

### 🔧 Planned Enhancements

* Integrate **ELK Stack** for enhanced log analysis
* Automate attack execution using **Python scripts**
* Implement **Wazuh SIEM** for better threat detection

### 🤝 How to Contribute

1. Fork the repository
2. Create a new branch with your improvements
3. Submit a pull request for review

---

## 📄 License

*This project currently has no license. You may add MIT License later to allow open use.*
