# NMAP The Basic – TryHackMe Walkthrough
Date Completed: Dec 31, 2025  
Category: Networking  
Difficulty: Easy  
Estimated Time: ~60 minutes  
Focus Areas: NMAP  
Goal: Learn how to use Nmap to discover live hosts, find open ports, and detect service versions  

## 📝 Introduction

This room provide a hands-on introduction to the NMAP network scanner. The objective is to understand how NMAP operates, explore its core scanning technique and apply it to real-worlds scenario.

## 📝 Task 2: Host Discovery – Who is Online
**Process:**  
- Ran `nmap -sn 192.168.0.1/27` to discover the last IP address within the subnet  
<img width="758" height="591" alt="list-live-host" src="https://github.com/user-attachments/assets/a56ed65d-18b1-46f3-8844-79326a76bc57" />

**Key Concepts:**  
- Nmap can be used to identify live host on both local or remote network
- Local Network Scan : NMAP start by sending an ARP request. If a device responds, NMAP labels it as "Host is up"
- Remote Network Scan : NMAP sent ICMP echo request (ping) to determine if host is online
	
**<ins>Command Examples:</ins>**  
`nmap -sn  192.168.0.1/27`       # Discover live host without probing services  
`nmap -sL  192.168.0.1/27`    # List target without actually scanning them  

**Reflection:**  
Nmap is a powerful tool for quickly enumerating devices on a network. Host discovery is often the first step in network reconnaissance, making it essential for both troubleshooting and security assessments

## Task 3: Port Scanning - Who is Listening
**Process:**  
  - Ran `nmap -sT 10.49.175.47` to enumerate active port on target
	<img width="631" height="250" alt="port-scanning" src="https://github.com/user-attachments/assets/e2c5f501-91f0-440a-843d-97d9a5a13872" />
	
**Key Concepts:** 

  - Port scanning can be perform either by using Connect Scan or Syn Scan (Stealth)  
  - Connect Scan (-sT) : NMAP attempts to complete three-way TCP handshake with each target TCP Port. This method is reliable but easier to be detected.  
  - Syn Scan (-sS) : NMAP send only the initial SYN packet without completing the handshake. This approach is faster and less likely to be logged  
	
**<ins>Command Examples:</ins>**  
`nmap -sT 10.49.175.47`       # TCP connect scan - complete three-way handshake  
`nmap -sS 10.49.175.47`    # TCP Syn - Initiate handshake without completion  

**Reflection:**   
Port scanning is a critical step in network reconnaissance. By identifying which ports are open and listening, analysts can determine potential entry points into a system and assess its exposure to threats.
