# Hacking Techniques and Countermeasures  
Hack The Box – Multi-Machine Penetration Testing Project

## Overview
This project documents a full end-to-end penetration testing engagement conducted against three vulnerable Windows-based machines on the Hack The Box platform. The objective was to demonstrate ethical hacking methodology, vulnerability identification, exploitation, and post-exploitation privilege escalation aligned with real-world penetration testing workflows.

## Skills Demonstrated
- Penetration testing methodology (Reconnaissance, Scanning, Exploitation, Post-Exploitation)
- Network and service enumeration
- Vulnerability assessment using CVSS
- Exploitation using Metasploit
- Windows privilege escalation
- Risk analysis and remediation planning
- Technical and management reporting

## Tools and Technologies
| Phase | Tools |
|-----|------|
| Reconnaissance | Nmap, Web Browser |
| Scanning | Nmap, Nessus |
| Exploitation | Metasploit, msfvenom |
| Post-Exploitation | Meterpreter |
| Platform | Hack The Box (PwnBox) |

## Methodology
The engagement followed a standard ethical hacking lifecycle:
1. Active reconnaissance to identify live hosts and exposed services  
2. Scanning for open ports, services, and known vulnerabilities  
3. Exploitation of identified weaknesses  
4. Post-exploitation privilege escalation  
5. Reporting and remediation recommendations  

## Target Machines and Findings

### Machine 1 – IIS 7.5 and Anonymous FTP
Key Findings:
- Anonymous FTP access enabled
- Outdated Microsoft IIS 7.5
- FTP command injection vulnerability (MS12-073)

Exploitation Summary:
- Uploaded an ASPX reverse shell via anonymous FTP
- Executed payload through the web server to obtain a Meterpreter session
- Privilege escalation to NT AUTHORITY\SYSTEM using ms10_015_kitrap0d

#### Screenshots:
<p align="center">
  Nmap Scan Results <br/>
  <img src="https://i.imghippo.com/files/ceS2068UbA.png"/>
  <img src="https://i.imghippo.com/files/NmY8720pIo.png"/>
</p>

<p align="center">
 FTP upload and Meterpreter session <br/>
  <img src="https://i.imghippo.com/files/EXz7509dRY.png"/>
</p>

### Machine 2 – Windows XP and SMB Vulnerabilities
Key Findings:
- Unsupported Windows XP operating system
- SMB vulnerabilities including MS08-067 and MS09-001
- SMB NULL session authentication enabled

Exploitation Summary:
- Exploited MS08-067 using Metasploit
- Achieved SYSTEM-level access via Meterpreter

Screenshots:
- SMB vulnerability detection
- Successful exploitation

### Machine 3 – IIS 6.0 on Windows Server 2003
Key Findings:
- Unsupported Windows Server 2003
- Outdated IIS 6.0 with WebDAV enabled
- Remote buffer overflow vulnerability

Exploitation Summary:
- Exploited IIS WebDAV buffer overflow vulnerability
- Migrated process to SYSTEM privileges
- Achieved full system compromise

Screenshots:
- Searchsploit results
- Privilege escalation confirmation

## Impact Analysis
If deployed in a production environment, these vulnerabilities could result in:
- Full system compromise
- Data breaches and ransomware attacks
- Regulatory non-compliance
- Financial and reputational damage

## Recommendations
- Upgrade unsupported operating systems to supported versions
- Migrate legacy IIS installations to IIS 10 or later
- Apply all critical Microsoft security patches
- Disable SMBv1 and enforce SMB signing
- Remove anonymous access to network services

## Research Extension – Generative AI in Reconnaissance
This project also examined how generative artificial intelligence can enhance the reconnaissance phase of penetration testing by automating large-scale port scanning, service enumeration, and adaptive reconnaissance strategies. A hybrid approach combining AI-assisted automation with human oversight is recommended.

## Screenshots
All supporting screenshots are stored in the screenshots directory and referenced throughout this document.

## Author
Emmanuel Ateji  
MSc Cyber Security  
Sheffield, United Kingdom  

GitHub: https://github.com/AtejiEmmanuel  
LinkedIn: https://linkedin.com/in/emmanuelateji

## Full Report
The complete academic report is included in this repository for reference and deeper technical detail.
