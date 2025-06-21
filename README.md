# SOC-Home-Lab-UTM-MacOS

> A fully virtualized, self-contained Security Operations Center (SOC) lab built using UTM on macOS. The lab simulates real-world attack and defense scenarios using Splunk (SIEM), Suricata (IDS), Nessus (vulnerability scanner), Sysmon (endpoint telemetry), and Splunk Universal Forwarder, distributed across three VMs.

---

##  Table of Contents

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

##  Project Overview

This repository provides a structured environment for blue teamers and SOC analysts to build detection engineering skills. Built entirely within **UTM on macOS**, this lab simulates:

* Endpoint-level telemetry collection (via Sysmon)
* Network-level intrusion detection (via Suricata)
* Centralized log correlation and analysis (via Splunk)
* Vulnerability scanning and posture evaluation (via Nessus)
* Attack simulation (via Kali Linux)

---

##  Architecture

**UTM Virtual Machines:**

* **Ubuntu Server**: Runs Splunk, Suricata IDS, and Nessus
* **Windows 10**: Configured with Sysmon and Splunk Universal Forwarder
* **Kali Linux**: Attacker simulation tools and payload generation

```text
Kali Linux(Attacker)------> Windows VM(Victim)------>UBUNTU VM (SOC SERVICES)
```

All VMs are connected via an **internal virtual LAN** within UTM.

---

##  Tools Used

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
## Step-by-Step Lab Configuration

---

### Step 1: Installing UTM and Creating Virtual Machines

#### **1.1 Installing UTM on macOS**

* Go to the official site: [https://mac.getutm.app](https://mac.getutm.app)
* Click **Download UTM** → install the `.dmg` file
* Drag and drop UTM into your **Applications** folder
* Launch UTM to begin creating your virtual machines

#### **1.2 Creating the Kali Linux VM**

* Download ISO: [https://www.kali.org/get-kali/](https://www.kali.org/get-kali/)
* Open UTM → Click **Create New VM**
* Choose:

  * **Virtualize** → Architecture: `ARM64 (aarch64)`
  * Attach ISO: Kali Linux ISO
  * Set RAM: 4 GB
  * CPU: 3 cores
  * Storage: 40 GB (dynamic recommended)
  * Network: Shared Network (Emulated VLAN)

#### **1.3 Creating the Ubuntu VM**

* Download ISO: [https://ubuntu.com/download/desktop](https://ubuntu.com/download/desktop)
* In UTM, repeat steps:

  * Choose Emulate
  * Architecture: `x86_64`
  * Attach Ubuntu 22.04/24.04 ISO
  * Set RAM: 6–8 GB
  * CPU: 4 cores
  * Storage: 60 GB
  * Network: Shared Network (Emulated VLAN)

#### **1.4 Creating the Windows 10 VM**

* Download ISO: [https://www.microsoft.com/en-us/software-download/windows10ISO](https://www.microsoft.com/en-us/software-download/windows10ISO)
* In UTM:

  * Choose Virtualize
  * Architecture: `ARM64 (aarch64)`
  * Attach Windows 10 ISO
  * Set RAM: 4 GB
  * CPU: 2 cores
  * Storage: 50 GB
  * Network: Shared Network (Emulated VLAN)

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

##  Next Steps & Contributions

###  Planned Enhancements

* Integrate **ELK Stack** for enhanced log analysis
* Automate attack execution using **Python scripts**
* Implement **Wazuh SIEM** for better threat detection

###  How to Contribute

1. Fork the repository
2. Create a new branch with your improvements
3. Submit a pull request for review

---

## 📄 License

*This project currently has no license. You may add MIT License later to allow open use.*
