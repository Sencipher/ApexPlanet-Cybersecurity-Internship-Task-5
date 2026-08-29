# Task 5 – Assessment Methodology

## Capstone Project: Vulnerability Assessment & Incident Response

This document describes the methodology followed during Task 5 of the ApexPlanet Cybersecurity & Ethical Hacking Internship.

All activities were performed in an isolated VMware lab environment using an intentionally vulnerable Metasploitable2 machine.

---

## 1. Lab Environment

| Component | Configuration |
|---|---|
| Attacker Machine | Kali Linux |
| Target Machine | Metasploitable2 |
| Attacker IP | `10.249.90.205` |
| Target IP | `10.249.90.76` |
| Virtualization | VMware Workstation |
| Testing Environment | Isolated Lab |

The objective was to identify vulnerabilities, validate selected findings through controlled exploitation, simulate incident response, apply defensive controls, and verify mitigation.

---

## 2. Assessment Workflow

The following methodology was used:

```text
Reconnaissance
      ↓
Service Enumeration
      ↓
Vulnerability Assessment
      ↓
Controlled Exploitation
      ↓
Post-Exploitation Validation
      ↓
Log Analysis
      ↓
Incident Response
      ↓
Containment
      ↓
Mitigation
      ↓
Verification
      ↓
Reporting
```

---

## 3. Reconnaissance & Service Enumeration

Nmap was used to identify open ports, running services, and service versions on the target.

Example:

```bash
nmap -sV -p 21 10.249.90.76
```

The assessment identified FTP running:

```text
21/tcp open ftp vsftpd 2.3.4
```

A broader scan also identified multiple exposed services on the intentionally vulnerable target.

Evidence:

`Screenshots/01_initial_nmap_scan.png`

`Screenshots/02_vsftpd_detection.png`

---

## 4. Vulnerability Assessment

Nmap vulnerability scripts were used to investigate identified services.

The FTP service was identified as vulnerable to the **vsftpd 2.3.4 backdoor vulnerability**.

### Identified Vulnerability

- **Service:** FTP
- **Software:** vsftpd 2.3.4
- **CVE:** CVE-2011-2523
- **Severity:** Critical
- **Status:** Exploitable in the lab environment

Evidence:

`Screenshots/03_vulnerability_scan.png`

---

## 5. Controlled Exploitation

Metasploit Framework was used to validate the vulnerability against the authorized Metasploitable2 target.

The following module was used:

```text
exploit/unix/ftp/vsftpd_234_backdoor
```

The vulnerability check indicated that the target appeared vulnerable.

Evidence:

`Screenshots/04_metasploit_check.png`

The vulnerability was then validated through controlled exploitation inside the isolated lab.

A Meterpreter session was successfully established.

Post-exploitation validation reported:

```text
Server username: root
```

This demonstrated the potential impact of the vulnerable FTP service.

Evidence:

`Screenshots/05_exploitation_root_access.png`

---

## 6. Log Analysis & Detection

Following exploitation, logs on the Metasploitable2 target were reviewed.

Authentication and connection-related entries were examined to identify activity associated with the assessment.

This stage simulated the **Detection and Analysis** phase of an incident-response process.

Evidence:

`Screenshots/06_log_analysis.png`

---

## 7. Incident Containment

After validating the vulnerability, a defensive firewall rule was applied to restrict access to TCP port 21.

```bash
sudo iptables -A INPUT -p tcp --dport 21 -j DROP
```

The firewall rules were reviewed to verify that the DROP rule had been applied.

Evidence:

`Screenshots/07_firewall_containment.png`

---

## 8. Eradication & Hardening

The vulnerable vsftpd service configuration was investigated as part of the hardening process.

Recommended permanent remediation includes:

- Removing or upgrading vsftpd 2.3.4
- Disabling unnecessary services
- Applying security patches
- Restricting network exposure
- Using secure administrative protocols
- Strengthening authentication
- Monitoring system and authentication logs

---

## 9. Post-Mitigation Verification

A follow-up Nmap scan was performed after containment.

The result showed:

```text
21/tcp filtered ftp
```

This confirmed that the network-level defensive control successfully restricted direct access to TCP port 21.

Evidence:

`Screenshots/08_post_mitigation_scan.png`

---

## 10. Findings Summary

| Finding | Severity | Action |
|---|---|---|
| vsftpd 2.3.4 Backdoor – CVE-2011-2523 | Critical | Remove/upgrade vulnerable service |
| Multiple legacy services exposed | High | Disable unnecessary services |
| Weak/legacy configurations | High/Medium | Harden services and protocols |
| Suspicious connection activity | High | Improve monitoring and alerting |

---

## 11. Incident Response Lifecycle

The simulated incident-response process followed:

1. **Detection** – Vulnerable FTP service identified.
2. **Analysis** – Vulnerability and system exposure assessed.
3. **Validation** – Controlled exploitation confirmed the security impact.
4. **Investigation** – Target logs were reviewed.
5. **Containment** – TCP port 21 was blocked.
6. **Eradication/Hardening** – Vulnerable service configuration was investigated.
7. **Recovery** – Network access was re-tested.
8. **Lessons Learned** – Remediation and monitoring recommendations were documented.

---

## 12. Conclusion

This methodology demonstrated an end-to-end vulnerability assessment and incident-response workflow in a controlled cybersecurity lab.

The project covered vulnerability discovery, controlled exploitation, evidence collection, log analysis, containment, mitigation, verification, and professional security reporting.

The exercise highlighted the importance of patch management, attack-surface reduction, network segmentation, security monitoring, and verification after remediation.

---

## Ethical Use Disclaimer

All testing described in this project was performed against an intentionally vulnerable machine inside an isolated lab environment.

The techniques documented here are intended strictly for educational and authorized cybersecurity testing purposes.
