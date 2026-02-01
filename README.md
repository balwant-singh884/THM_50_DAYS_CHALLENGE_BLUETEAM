
# 🛡️ NFS Stolen Mount PCAP Analysis (Blue Team Project)

## 📌 Project Overview

This project documents my investigation of a network capture (PCAP) involving unauthorized access to an NFS (Network File System) share. The objective was to identify the attacker, understand what files were accessed or stolen, and demonstrate a real-world SOC-style workflow.

This project is based on the **"Stolen Mount"** room from TryHackMe and reflects practical Blue Team analysis skills.

---

## 🎯 Objectives

* Identify suspicious NFS activity in a PCAP file
* Determine the source (attacker) and destination (server)
* Track file access, read, write, and delete operations
* Extract and analyze transferred data
* Build a structured incident analysis report

---

## 🧰 Tools Used

* **Wireshark** – Packet capture analysis
* **CyberChef (Web Version)** – Data decoding and file extraction
* **Linux CLI Tools** – `strings`, `file`, `xxd`, `base64`

---

## 🔍 Step-by-Step Analysis Workflow

### 1️⃣ Initial PCAP Review

* Opened the PCAP file in Wireshark
* Scanned the **Protocol** column to identify dominant protocols
* Observed **RPC and NFS** traffic patterns

---

### 2️⃣ Protocol Filtering

Used simple protocol-based filters:

```
nfs
rpc
```

This isolated all NFS and mount-related traffic.

---

### 3️⃣ Identifying Client and Server

* Analyzed **Source and Destination IP addresses**
* Identified which host initiated the mount request
* Mapped communication between the client and NFS server

---

### 4️⃣ Tracking Suspicious File Operations

Focused on operations such as:

* File reads
* File writes
* File deletions

Observed abnormal access patterns indicating possible data exfiltration.

---

### 5️⃣ Following Sessions

Used:

* **Follow → TCP Stream**
* **Follow → UDP Stream**

This allowed reconstruction of complete sessions and file transfers.

---

### 6️⃣ Data Extraction

* Exported raw data from streams
* Analyzed extracted files using:

```bash
strings file.bin
file file.bin
xxd file.bin | less
```

* When local CyberChef failed, used the **online CyberChef tool** for decoding

---

## 🚨 Key Findings

* Unauthorized NFS mount detected
* Suspicious client IP identified
* Sensitive files accessed and transferred
* Evidence of potential data exfiltration

---

## 🧠 Skills Gained

* PCAP analysis using a SOC mindset
* Protocol discovery and filtering
* Network file system investigation
* Data extraction and decoding
* Incident analysis and documentation

---

## 📁 Repository Structure

```
NFS-Stolen-Mount-Analysis/
├── README.md
├── pcap/
│   └── stolen_mount.pcap
├── extracted_files/
│   └── suspicious_data.bin
├── analysis_notes/
│   └── investigation_steps.md
└── screenshots/
    └── wireshark_filters.png
```

---

## 🏁 Conclusion

This project demonstrates practical Blue Team skills required for SOC roles, including packet analysis, threat investigation, and evidence-based reporting. It reflects real-world incident response workflows and tool adaptability when primary tools fail.

---

## 📫 Author

**Balwant Singh**
Cybersecurity Student | Blue Team | SOC Analyst Aspirant

---

## 🔗 Acknowledgment

Project inspired by the **TryHackMe "Stolen Mount"** room.
