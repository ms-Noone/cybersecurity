# NMAP The Basic – TryHackMe Walkthrough
Date Completed: Dec 31, 2025  
Category: Networking  
Difficulty: Easy  
Estimated Time: ~60 minutes  
Focus Areas: NMAP  
Goal: Learn how to use Nmap to discover live hosts, find open ports, and detect service versions  

## 📝 Overview

Hands-on lab focused on Nmap basics — host discovery, port scanning, and service version detection. Objective was to practice reconnaissance techniques connect findings to vulnerability assessment in SOC workflows

## 📝 Task 2: Host Discovery – Who is Online
**<ins>Commands:</ins>**  
`nmap -sn  192.168.0.1/27`       # Discover live host without probing services  
`nmap -sL  192.168.0.1/27`    # List target without actually scanning them  

<img width="758" height="591" alt="list-live-host" src="https://github.com/user-attachments/assets/a56ed65d-18b1-46f3-8844-79326a76bc57" />

**Result:**  
Identified **32 active host** in subnet

**Analysis:**  
Enumerating device is the first step in network reconnaisance. This process helps analyst establish baseline visibility, identify potential attack surface and prioritize systems for security assessment

## 📝Task 3: Port Scanning - Who is Listening
**<ins>Command:</ins>**  
`nmap -sT 10.49.175.47`       # TCP connect scan - complete three-way handshake  

<img width="631" height="250" alt="port-scanning" src="https://github.com/user-attachments/assets/e2c5f501-91f0-440a-843d-97d9a5a13872" />
	
**Result:**  
Found **6 open ports**: 7 (ECHO), 9 (Discard), 13 (Daytime), 17(QOTD) , 22 (SSH), 8008 (HTTP)
	
**Analysis:**  
Identified 4 legacy services (Echo, Discard, Daytime and QOTD). Outdated services increase the system's attack surface and may serve as entry point for DOS or reflection attacks



## 📝Task 4: Version Detection – Extract More Information##  
**<ins>Command:</ins>**  
`nmap -sS -sV 10.48.153.79` #TCP Syn with Service version detection

<img width="861" height="215" alt="Version-detection" src="https://github.com/user-attachments/assets/bb673248-5e82-4d6f-8d86-6697cebdf3e0" />  

`nmap -sS -O 10.48.153.79` #TCP Syn with OS fingerprinting

<img width="826" height="358" alt="OS-fingerprinting" src="https://github.com/user-attachments/assets/889a53a9-92fa-4931-a48d-e9487dce9e36" />  

**Result:**  
Detected 3 outdated services and a legacy OS: 
- LANDesk remote management  → linked to [CVE-2010-2892](https://www.cvedetails.com/cve/CVE-2010-2892/)
- lighttpd 1.4.74 → outdated web server with potential web exploitation risks
- OpenSSH 9.6p1 Ubuntu 3Ubuntu13.5 → linked to [CVE-2024-6387](https://ubuntu.com/security/cve-2024-6387)
- Linux kernel 4.15 → End-of-Life and no longer receive security patches [Vulnerability](https://www.cvedetails.com/version/564832/Linux-Linux-Kernel-4.15.html)
	
**Analysis:**  
Version detection identified outdated and vulnerable services that expand the system's attack surface. These findings demonstrate how service enumeration supports vulnerability assessment, guiding patching priorities and defensive hardening in SOC workflows 
 

## 📝Task 5: Timing - How Fast is Fast  
**Concepts Learned:**  
NMAP provides timing templates that can control scan speed and stealth  
| Timing | Use Case | SOC Impact |  
|--------|----------|------------|  
| T0 (Paranoid) | Extremely slow | Avoids detection, impractical for large scans |  
| T1 (Sneaky)   | Very slow | Minimizes IDS alerts |  
| T3 (Normal)   | Default | Balanced speed vs detection risk |  
| T4 (Aggressive) | Fast | Useful internally, may trigger alerts |  
| T5 (Insane)   | Very fast | Likely detected, for troubleshooting only | 

**Application example:**  
Used -T0 or -T1 to evade from detection during reconnaisance, Analyst can also apply these template to test the specific firewall rule and observe how different speed affect IDS/IPS responses

## 📝Task 6: Output – Controlling What You See
**Concepts Learned:**  
  - NMAP provides switches that help to Analyst to control scan output
    | Option  | Description |
	| ------------- | ------------- |
	| -v | Provide real-time details about scan progress |
    | -d | Useful for troubleshooting when NMAP not behaving as expected (intended for developer) |
	| -oN filename |	Save Scan Report to Normal Output |
	| -oX filename |	Save Scan Report to XML Output |
	| -oG filename |	Save Scan Report to grep-able output |
	| -oA filename |	Save Scan Report to output in all major format (.nmap, .gnamp, .xml) |

**Application example:**  
Using the -v option helps analyst gain real-time visibility of scan process, this is valuable during long or complex scan.The `-oA` option is valuable for saving results in multiple formats, supporting incident documentation and further analysis in SOC workflows.

## 📝 Key Takeways
NMAP is one of the most widely used tools in Reconnaissance, exploring its feature help me to understand how analysts can enumerate targets, identify services, and assess potential vulnerabilities. This knowledge strengthens defensive strategies and prepares me for real‑world SOC analyst responsibilities.  




