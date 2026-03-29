# Hacking Techniques and Countermeasures: Penetration Testing Report

A structured penetration testing report covering the full ethical hacking lifecycle across three target machines on the [Hack The Box](https://www.hackthebox.com/) platform. This project was completed as part of a cybersecurity assessment and demonstrates hands-on application of industry-standard tools and methodology.

---

## Overview

This project documents the reconnaissance, scanning, exploitation, and post-exploitation phases carried out against three Windows-based machines in an isolated lab environment. Each machine presented a unique attack surface, and the report details the exact steps taken to identify vulnerabilities, exploit them, and escalate privileges to NT AUTHORITY\SYSTEM level.

An additional section explores the use of **Generative AI to automate the reconnaissance phase** of penetration testing, discussing its advantages, limitations, and practical recommendations.

---

## Methodology

The penetration testing process followed a four-phase approach:

```
Reconnaissance → Scanning → Exploitation → Post-Exploitation
```

| Phase | Description |
|---|---|
| **Reconnaissance** | Active information gathering using Nmap to identify hosts, open ports, and running services |
| **Scanning** | Port scanning and vulnerability scanning using Nmap scripts and Nessus |
| **Exploitation** | Using Metasploit and msfvenom to exploit discovered vulnerabilities and gain initial access |
| **Post-Exploitation** | Privilege escalation to SYSTEM level using local exploit suggester modules |

---

## Machines Tested

### Machine 01290095 (`10.129.192.180`)
- **OS:** Windows 7 (6.1 Build 7600)
- **Open Ports:** 21 (FTP), 80 (HTTP)
- **Key Vulnerability:** Anonymous FTP login enabled on Microsoft IIS 7.5; CVE-2015-1635 (HTTP.sys RCE)
- **Exploit:** Uploaded a malicious `.aspx` reverse shell via anonymous FTP, triggered via the web browser, caught with Metasploit's `multi/handler`
- **Privilege Escalation:** `ms10_015_kitrap0d` - escalated to `NT AUTHORITY\SYSTEM`

---

### Machine 01280094 (`10.129.192.201`)
- **OS:** Windows XP SP3
- **Open Ports:** 135 (RPC), 139 (NetBIOS), 445 (SMB)
- **Key Vulnerabilities:** MS08-067 (RPC RCE), MS17-010 (EternalBlue), SMB NULL session authentication, SMB signing not enforced
- **Exploit:** Exploited MS08-067 via Metasploit's `exploit/windows/smb/ms08_067_netapi` to obtain a Meterpreter shell
- **Privilege Escalation:** Already `NT AUTHORITY\SYSTEM` on initial access

---

### Machine 012B0096 (`10.129.192.204`)
- **OS:** Windows Server 2003 SP2
- **Open Ports:** 80 (HTTP / WebDAV)
- **Key Vulnerabilities:** IIS 6.0 WebDAV PROPFIND buffer overflow (CVE-2017-7269), unsupported OS and web server
- **Exploit:** Metasploit module `exploit/windows/iis/iis_webdav_scstoragepathfromurl` to obtain Meterpreter shell, followed by process migration to NT AUTHORITY context
- **Privilege Escalation:** `ms10_015_kitrap0d` - escalated to `NT AUTHORITY\SYSTEM`

---

## Tools Used

| Tool | Purpose |
|---|---|
| **Nmap** | Active reconnaissance, port scanning, vulnerability detection (`--script vuln`) |
| **Nessus** | Vulnerability scanning with CVSS scoring |
| **Metasploit / msfconsole** | Exploitation framework, payload delivery, post-exploitation |
| **msfvenom** | Payload generation (`.aspx` reverse shell) |
| **Meterpreter** | Post-exploitation shell: privilege escalation, system enumeration |
| **Firefox** | Navigating web services discovered during scanning |
| **FTP client** | Uploading payloads to anonymous FTP services |

---

## Vulnerability Summary

| Machine | Vulnerability | Severity | CVSS |
|---|---|---|---|
| 01290095 | Unsupported Web Server (IIS 7.5) | Critical | 10.0 |
| 01290095 | MS12-073 FTP Command Injection | Medium | 5.3 |
| 01280094 | MS08-067 RPC RCE | Critical | 9.8 |
| 01280094 | Windows XP End of Life | Critical | 10.0 |
| 01280094 | MS17-010 (EternalBlue/WannaCry) | High | 8.1 |
| 01280094 | SMB NULL Session Authentication | High | 7.3 |
| 01280094 | SMB Signing Not Required | Medium | 5.3 |
| 012B0096 | IIS 6.0 WebDAV PROPFIND RCE (CVE-2017-7269) | Critical | 9.8 |
| 012B0096 | Windows Server 2003 End of Life | Critical | 10.0 |
| 012B0096 | Microsoft IIS 6.0 End of Life | Critical | 10.0 |

---

## Key Recommendations

- **Upgrade operating systems:** Replace Windows XP and Server 2003 with a supported OS (Windows 10 / Server 2019 or later)
- **Update IIS:** Migrate from IIS 6.0 / 7.5 to IIS 10, which resolves hundreds of known vulnerabilities
- **Disable anonymous FTP:** Remove unauthenticated access to file services
- **Patch critical CVEs:** Apply MS08-067, MS17-010, and MS12-073 patches immediately
- **Enforce SMB signing:** Enable `Microsoft network server: Digitally sign communications (always)` via Group Policy
- **Disable SMBv1:** SMBv1 is a deprecated protocol exploited by WannaCry and EternalBlue attacks
- **Restrict SMB NULL sessions:** Set `RestrictAnonymous = 1` in the registry to prevent unauthenticated enumeration
- **Disable WebDAV:** If not required, disable WebDAV on IIS to eliminate the PROPFIND attack surface

---

## Generative AI & Reconnaissance

The report includes a research section examining how **Generative AI** (GPT-style language models, GANs, reinforcement learning) can automate the reconnaissance phase of penetration testing.

**Key takeaways:**
- AI enables broader port/service coverage and tireless, systematic scanning at scale
- Reinforcement learning agents can discover novel scanning strategies beyond human imagination
- GAN-generated payloads can mutate syntax to evade signature detection
- Risks include destabilisation of production systems, abuse by malicious actors, and harder-to-audit reasoning
- A **hybrid approach** (AI for scale, humans for validation and creativity) is recommended

---

## Disclaimer

> This project was carried out entirely within the **Hack The Box** lab environment using their **PwnBox** platform. All testing was performed on machines explicitly provided for this purpose. No real-world systems were targeted. This report is intended purely for **educational purposes** and to demonstrate ethical hacking methodology in a controlled setting.

---

## References

Key references include:
- Engebretson, P. (2013). *The Basics of Hacking and Penetration Testing*. Elsevier.
- Microsoft Security Bulletins: MS08-067, MS09-001, MS12-073, MS17-010
- Tenable Nessus Plugin documentation
- CrowdStrike (2023). *Generative AI and its impact in cybersecurity*
- George, S., Douglas, T., & William, E. (2021). *Using AI/ML for Reconnaissance in Network Penetration Testing*. Academic Conferences International.

Full reference list available in the (report document)[https://github.com/AtejiEmmanuel/Hack-The-Box-Multi-Machine-Penetration-Testing-Project/blob/main/33043543_Emmanuel_HTC_2023.docx].
