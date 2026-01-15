# TCPDump – TryHackMe Walkthrough

**Room** : [TCPDump The Basic](https://tryhackme.com/room/tcpdump)  
**Date Completed** : Jan 8, 2026   
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

## 📝Task 3: Filtering Expression
**Packet file used:**  
traffic.pcap  

**Commands:** 
- `tcpdump -r traffic.pcap icmp | wc`  # filter ICMP packets and count lines
   <img width="608" height="86" alt="icmp_total_packet" src="https://github.com/user-attachments/assets/60f50a7e-aec2-4d60-8d3b-1d4d2d385b22" />

- `tcpdump -r traffic.pcap arp` # filter ARP packets
  <img width="886" height="141" alt="mac" src="https://github.com/user-attachments/assets/88d57a65-5f41-4b98-924c-726ed279e015" />
  
- `tcpdump -r traffic.pcap udp port 53` #filter DNS packet on UDP port 53
  <img width="1897" height="402" alt="udp" src="https://github.com/user-attachments/assets/e23fc766-b3bd-43ed-9632-1c99d2a2a54b" />

**Result:**  
- Displayed packet specific to the requested protocol (ICMP, ARP, DNS)
- Reduced noise compared to full capture, focusing only on relevant traffic
  
**Analysis:**  
Packet filtering helps analysts isolate suspicious traffic for deeper investigation.  By applying filtering expression, analyst can:
- **Incident Investigation** → Focus on traffic tied to alerts (e.g., ICMP scans, ARP spoofing, DNS anomalies)  
- **Evidence Collection** → Capture only relevant packets, reducing file size and improving clarity for forensic review 
