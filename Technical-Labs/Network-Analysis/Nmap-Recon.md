# NMAP – Network Reconnaissance & Vulnerability Discovery

**Category:** Network Security / Offensive Operations  
**Lab Environment:** TryHackMe & Home Lab (Metasploitable 2)  
**Focus Areas:** Service Enumeration, Scripting Engine (NSE), and Vulnerability Mapping
  
## 📝 Overview

This project documents the application of Nmap for host discovery and service auditing. The objective was to move beyond simple port scanning to perform vulnerability mapping by correlating service versions with known CVEs (Common Vulnerabilities and Exposures).  

## 📝 Phase 1: Enumeration
### _1.1 Host Discovery_
**<ins>Commands:</ins>**  
`nmap -sn  192.168.0.1/27`        

**Purpose:**  
Discover live host without probing services and without triggering heavy security alerts

<img width="558" height="73" alt="image" src="https://github.com/user-attachments/assets/5b2b9dcd-7b36-4995-b6f2-0311c89da84b" />

**Result:**  
Identified **32 active hosts** in subnet

**Analysis:**  
Enumerating devices is the first step in network reconnaisance. This process helps analyst establish baseline visibility, identify potential attack surface and prioritize systems for security assessment

### _1.2 Service Auditing & Attack Surface Identification_
**<ins>Command:</ins>**  
`nmap -sT -p- 10.48.167.166`       # TCP connect scan - complete three-way handshake  

**Purpose:**  
Connect scan by complete the TCP three-way handshake with every target TCP port 

<img width="580" height="247" alt="image" src="https://github.com/user-attachments/assets/f84d0741-9dc3-4ab0-bdce-e0602db3eb75" />

**Result:**  
Found **6 open ports**: 7 (ECHO), 9 (Discard), 13 (Daytime), 17(QOTD) , 22 (SSH), 8008 (HTTP)
	
**Analysis:**  
- Legacy services (Echo, Discard, Daytime, QOTD): Rarely used today, increase attack surface, and may be exploited for DoS/reflection attacks.
- SSH (22): Common attack vector, requires monitoring for brute‑force attempts.
- HTTP (8008): Potential entry point for web exploitation.

 **Remediation:** 
 - Disable legacy services to reduce attack surface
 - Patch web service to mitigate exploitation risk
 - Harden SSH with strong authentication

### _1.3 Deep Dive: Version Detection & CVE Mapping_
**<ins>Command:</ins>**  
`nmap -sS -sV -O 10.48.167.166`

**Purpose:**  
To discover Service, Version and OS detection, or we can also change it to `-A` which enables OS detection, version scanning, and traceroute, among other things  

<img width="1395" height="906" alt="image" src="https://github.com/user-attachments/assets/07665819-6e60-4b59-9751-c7de20d9575c" />


**Result:**  
Detected 3 outdated services and a legacy OS: 
- LANDesk remote management  → linked to [CVE-2010-2892](https://www.cvedetails.com/cve/CVE-2010-2892/)
- lighttpd 1.4.74 → outdated web server with potential web exploitation risks
- OpenSSH 9.6p1 Ubuntu 3Ubuntu13.5 → linked to [CVE-2024-6387](https://ubuntu.com/security/cve-2024-6387)
- Linux kernel 4.15 → End-of-Life and no longer receive security patches [Vulnerability](https://www.cvedetails.com/version/564832/Linux-Linux-Kernel-4.15.html)
	
**Analysis:**  
Version detection identified outdated and vulnerable services that expand the system's attack surface. These findings demonstrate how service enumeration supports vulnerability assessment, guiding patching priorities and defensive hardening in SOC workflows 

 **Remediation:** 
 - Upgrade or replace LANDesk and lighttpd services.
 - Priotizing OpenSSH patching update
 - Migrate frim Linux kernel 4.15 to a supported or latest version to ensure ongoing security updates

## 📝 Phase 2: Real-World Lab Application (Metasploitable 2)

To practice these techniques, I ran a targeted scan against a Metasploitable2 VM in my home lab. This exercise focuses on service and version detection, along with mapping vulnerabilities to known CVEs using the Nmap Scripting Engine(NSE)  

**<ins>Command:</ins>**  
`nmap -sV -sC --script vuln -oN blue.nmap 192.168.1.5`

**Finding:**  
- Identify around ~23 open port, one of it is **vsftpd 2.3.4** running on port 21
- The scan output flagged CVE-2011-2523 for this service. Cross-referencing with Exploit-DB confirmed that this version contains Backdoor Vulnerability(CVE-2011-2523). This allows an attacker to spawn a shell by sending a username ended with :)

 **Remediation:** 
 - Isolate the vulnerable host and apply the relevant patch, or migrate to SSH File Transfer Protocol (SFTP) which provide secure file transfer over an encrypted channel
 - Implement firewall rule to restrict port 21 access to authorized IPs address only

## 📝 Key Takeways
- NMAP is not just a scanner, it is a tools that we use for reconnaissance to gather info and identify vulnerabilites
- Utilizing the -oA flag ensures that scan results are preserved in XML, Grepable, and Normal formats, which is essential for audit trails and incident response

 **Cheatsheet:**  
Refer this [cheatsheet](https://github.com/ms-Noone/cybersecurity/blob/main/Cheatsheet/NMAP.md) for other usefull command in Nmap

