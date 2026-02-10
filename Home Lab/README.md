# Cybersecurity Home Lab Setup

## Overview
This home lab project is designed to replicate a small enterprise environment for practicing penetration testing. The setup consists of Kali Linux, as the attacker machine and Metasploitable 2 as the target system. The primary objective is to practice penetration testing and vulnerability assessments within a secure, controlled virtual machine.  

## Lab Environment & Architecture

The lab is hosted on Oracle Virtual Box, with all virtual machines connected through a Nat Network. This configuration to ensures the lab remains isolated and protected from external network exposure.

<img width="768" height="768" alt="Modern Pastel Flowchart" src="https://github.com/user-attachments/assets/13acde51-2e9b-418d-a3cb-b483692c0c3b" />

# Scope
| System Role | Operating System | IP  |
| ------------- | ------------- | ------------- |
| Attacker | Kali Linux | 192.168.1.4  |
| Target | Metasploitable 2  | 192.168.1.5  |

## Tools
The following tools were used during assessment:
1. Nmap: Used for network discovery, port scanning and vulnerability assessment
2. Metasploit Framework: Applied to exploit identified vulnerabilities found by Nmap

## Techniques
The following techniques were used during assessment:
1. Scanning and Enumeration
   - Conducted port scans and service enumeration using Nmap
   - Identified potential vulnerabilities for exploitation
2. Exploitation
   - Leveraged Metasploit Framework to exploit discovered vulnerabilities
   - Validated successful compromise of the target system

## Walkthrough
[Metasploitable2_Walkthrough](https://github.com/ms-Noone/cybersecurity/blob/main/Home%20Lab/Metapsploitable2_Walkthrough.md)
