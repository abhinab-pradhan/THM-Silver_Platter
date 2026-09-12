# 🥈 TryHackMe — Silver Platter

> **Silverpeas | Authentication Bypass | IDOR | Credential Exposure | Linux Privilege Escalation**

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-55a630?style=flat-square&labelColor=555555)
![Platform](https://img.shields.io/badge/Platform-TryHackMe-00a98f?style=flat-square&labelColor=555555)
![Vulnerability](https://img.shields.io/badge/Vulnerability-Auth%20Bypass%20%7C%20IDOR-f06c2f?style=flat-square&labelColor=555555)
![Service](https://img.shields.io/badge/Service-HTTP%20%7C%20SSH-008cc1?style=flat-square&labelColor=555555)
![OS](https://img.shields.io/badge/OS-Ubuntu-e95420?style=flat-square&labelColor=555555)

---

## 📋 Overview

**Silver Platter** is a TryHackMe Linux machine focused on web application enumeration, Silverpeas vulnerabilities, credential exposure, and Linux privilege escalation.

The machine demonstrates a multi-stage attack chain:

```text
Reconnaissance
      ↓
Web Enumeration
      ↓
Silverpeas Discovery
      ↓
Authentication Bypass
      ↓
Broken Access Control / IDOR
      ↓
Credential Disclosure
      ↓
SSH Access
      ↓
Log Enumeration
      ↓
Credential Reuse
      ↓
Privilege Escalation
      ↓
     Root

```

---

## 🎯 Objectives
-- Enumerate the target system.
-- Identify exposed services.
-- Discover the Silverpeas application.
-- Exploit the authentication mechanism.
-- Abuse broken access control in Silverpeas.
-- Obtain valid SSH credentials.
-- Gain access as **tim**.
-- Enumerate the Linux system.
-- Identify credentials exposed in logs.
-- Switch to **tyler**.
-- Escalate privileges to **root**.
-- Capture the user and root flags.

---

## 🔎 1. Reconnaissance

I started with an Nmap service/version scan:
```
nmap -sV 10.49.136.131
```
**Results**
```
22/tcp    open    ssh         OpenSSH 8.9p1 Ubuntu
80/tcp    open    http        nginx 1.18.0
8080/tcp  open    http-proxy
```

<img width="1168" height="633" alt="1" src="https://github.com/user-attachments/assets/5d5d3971-13b3-4b91-876e-e270c0ae0617" />


The target was running Ubuntu and exposed two HTTP services along with SSH.

**Attack Surface**
```
22/tcp   → SSH
80/tcp   → Web application
8080/tcp → Web application / Silverpeas
```

## 🌐 2. Web Enumeration

I visited the website running on port 80:
```
http://10.49.136.131
```
The website was titled:
```
Hack Smarter Security
```
The public website contained a **Contact** section.

<img width="1089" height="712" alt="2" src="https://github.com/user-attachments/assets/d933d623-70c8-4e68-b5e9-46109fc0c02f" />



## 👤 3. Information Disclosure

The Contact page revealed information about the organization's project manager.

It specifically mentioned:
```
Silverpeas
```
and disclosed the username:
```
scr1ptkiddy
```

<img width="1037" height="615" alt="2-1" src="https://github.com/user-attachments/assets/b635b50a-5cbb-430a-af24-212cd476c469" />

**Why this was important**

This gave us two useful pieces of information:
```
Application → Silverpeas
Username    → scr1ptkiddy
```
This demonstrates why manual web enumeration is important. Public-facing pages can disclose usernames and information about the technologies used by an organization.

