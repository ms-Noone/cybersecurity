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
