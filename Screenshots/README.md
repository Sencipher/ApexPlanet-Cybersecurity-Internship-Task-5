
# 📸 Task 5 – Evidence Screenshots

This folder contains evidence collected during the **Task 5 Capstone Project – Vulnerability Assessment & Incident Response**.

All testing was performed in an isolated VMware lab using Kali Linux and an intentionally vulnerable Metasploitable2 machine.

## Screenshot Evidence

| # | Screenshot | Description |
|---|---|---|
| 01 | `01_initial_nmap_scan.png` | Initial Nmap enumeration showing exposed ports and services on Metasploitable2. |
| 02 | `02_vsftpd_detection.png` | Focused Nmap scan identifying FTP running vsftpd 2.3.4 on TCP port 21. |
| 03 | `03_vulnerability_scan.png` | Vulnerability scan identifying the vsftpd 2.3.4 backdoor (CVE-2011-2523). |
| 04 | `04_metasploit_check.png` | Metasploit validation showing that the target appears vulnerable. |
| 05 | `05_exploitation_root_access.png` | Controlled exploitation demonstrating a successful session and root-level access. |
| 06 | `06_log_analysis.png` | Target-side log analysis used during the incident investigation. |
| 07 | `07_firewall_containment.png` | Defensive containment using an iptables DROP rule for TCP port 21. |
| 08 | `08_post_mitigation_scan.png` | Verification scan showing TCP port 21 as filtered after containment. |

## Assessment Flow

`Reconnaissance → Vulnerability Detection → Validation → Controlled Exploitation → Log Analysis → Containment → Verification`

> **Disclaimer:** These screenshots document authorized testing performed only in an isolated cybersecurity training environment.
