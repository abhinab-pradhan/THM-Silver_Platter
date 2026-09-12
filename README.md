## 🥈 Silver Platter — TryHackMe Write-Up
**Silverpeas | Authentication Bypass | IDOR / Broken Access Control | Credential Exposure | Linux Privilege Escalation**

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)
![Platform](https://img.shields.io/badge/Platform-Linux-red)
![Status](https://img.shields.io/badge/Status-Pwned-success)

## 📌 Overview
This write-up documents the full exploitation chain of the **Silver Platter** machine. The attack path is a classic multi-stage penetration test involving:
1.  **Network & Web Enumeration:** Identifying exposed services and reconnaissance.
2.  **Web Application Exploitation:** Leveraging two distinct vulnerabilities in the *Silverpeas* application (Authentication Bypass & IDOR).
3.  **Credential Harvesting:** Extracting SSH credentials from application logs.
4.  **Linux Privilege Escalation:** Moving from a low-privileged user to root via log analysis and sudo abuse.

The machine demonstrates how a seemingly secure web application can serve as the entry point for a complete system compromise.

