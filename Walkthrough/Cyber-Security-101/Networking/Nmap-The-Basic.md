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
Found 6 open ports: 7 (ECHO), 9 (Discard), 13 (Daytime), 17(QOTD) , 22 (SSH), 8008 (HTTP)
	
**Analysis:**  
Identified 4 legacy services (Echo, Discard, Daytime and QOTD). Outdated services increase the system's attack surface and may serve as entry point for DOS or reflection attacks



## 📝Task 4: Version Detection – Extract More Information##  
**Process:**  
  - Ran `nmap -sS -sV 10.48.153.79` to identify open port and detect the versions of service version 
	<img width="840" height="191" alt="Version-detection" src="https://github.com/user-attachments/assets/b79acb8b-a9e9-49da-9bed-39e889e89d23" />

**Key Concepts:**  
  - OS Detection (-O): Attempts to fingerprint the operating system running on the target.
  - Service Version Detection (-sV): Nmap probes open ports to determine the software and version associated with each service.
  - Combining port scanning with -sV provide deeper insight into service bound to ports, such as http, ssh daemon and etc
	
**<ins>Command Examples:</ins>**
`nmap -sS 10.49.175.47`    # TCP Syn(Stealthily - Initiate handshake without completion  
`nmap -sS -O 10.49.175.47`       # Attempt OS fingerprinting
`nmap -sS -sV 10.49.175.47`    # Syn Scan with Service version detection

## 📝Task 5: Timing - How Fast is Fast  
**Overview:**  
Timing controls are critical because scan speed can influence detection by Intrusion Detection Systems (IDS) or other security solutions.

**Key Concepts:**  
  - NMAP at default speed may trigger alerts in IDS or other security solution  
  - To avoid been detect, NMAP provide timing templates (T0 - T5)  
    | Timing  | Description |
	| ------------- | ------------- |
	| T0 (paranoid) |	Extremely slow, designed to avoid detection |
	| T1 (sneaky) |	Very slow, minimizes IDS alerts |
	| T2 (Polite) |	Slows down to reduce network load |
	| T3 (Normal) |	Default speed, balanced |
	| T4 (Aggressive) |	Faster scans, may trigger detection |
	| T5 (Insane) |	Very fast, likely to be detected |


## 📝Task 6: Output – Controlling What You See
**Overview:**  
Output control is essential for monitoring scan progress, troubleshooting, and saving results for later analysis.

**Key Concepts:**  
  - Verbosity (-v) :  Provide real-time details about scan progress. With this option, Analyst can observe how NMAP transition through different stages such as ARP Ping scan, DNS resolution & TCP Syn attempt on each open port  
  - Debugging (-d) : useful for troubleshooting when NMAP not behaving as expected (intended for developer)
  - Saving Scan Reports: Nmap supports multiple output formats:
    | Option  | Description |
	| ------------- | ------------- |
	| -oN filename |	Normal Output |
	| -oX filename |	XML Output |
	| -oG filename |	grep-able output |
	| -oA filename |	output in all major format (.nmap, .gnamp, .xml) |
	

## 📝 Key Takeways
NMAP is one of the most widely used tools in Reconnaissance, exploring its feature help me to understand how analysts can enumerate targets, identify services, and assess potential vulnerabilities. This knowledge strengthens defensive strategies and prepares me for real‑world SOC analyst responsibilities.  




