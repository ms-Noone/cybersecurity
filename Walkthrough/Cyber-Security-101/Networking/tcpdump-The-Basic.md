# TCPDump – TryHackMe Walkthrough

**Room** : [TCPDump The Basic](https://tryhackme.com/room/tcpdump)  
**Date Completed** : Jan 8, 2025  
**Category** : Networking  
**Focus Areas** : Command Line Packet capture  

## 📝 Overview  
Hands-on lab focused on TCPDump fundamentals:  
- Capture packet via command line  
- Apply filters to isolate relevant traffic  
- Control how captured packets are displayed for analysis

**Objective:**  
Develop practical command‑line packet analysis skills with TCPDump, while understanding when to use it versus Wireshark in network traffic analysis

## 📝 Task 2: Basic Packet Capture
**Commands:**  
`sudo tcpdump -i ens5 -c 5 -n`  #Capture 5 packets on ens5 without resolving IP address  

<img width="1891" height="273" alt="basic" src="https://github.com/user-attachments/assets/ce5e7b71-8599-4faa-990a-eb88298386fb" />

**Result:**  
- Displayed packet details of specific network interface  
- IP address shown directly without making DNS lookup  

**Analysis:**  
Understanding TCPDump's basic syntax is essential for effective use of the tool. The -n option prevents DNS resolution which reduces overhead by avoiding unnecessary lookups and enables faster triage
