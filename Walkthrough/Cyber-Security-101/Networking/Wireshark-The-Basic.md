# Wireshark -Tryhackme Walkthrough

**Room:** [Wireshark The Basic](https://tryhackme.com/room/wiresharkthebasics)  
**Date Completed:** Jan 7, 2026  
**Category:** Networking  
**Focus Areas:** Wireshark  

## 📝 Overview  

This hands-on lab focused on Wireshark fundamentals, including:  
- Navigate and configure Wireshark interface
- Inspect packet to extract information
- Apply display filter to isolate relevant traffic.

**Packet file used:**  
- Exercise.pcapng  
  
**Objective:**  
Practice network analysis and deepen understanding of protocols within the packet capture. These skills are critical in SOC workflows for detecting anomalies, investigating suspicious traffic, and validating security events.  

## 📝 Task 2: Tool Overview

**Process:**  
	1. Open the capture file in Wireshark  
	2. Reviewed file metadata via **Capture File Properties**    
<img width="1916" height="966" alt="File-Properties" src="https://github.com/user-attachments/assets/346a82c1-47b6-44f6-8eda-7e21bebd0ade" /><br />

**Result:**  
- File comment contained flag → **TryHackMe_Wireshark_Demo**
- Total Packet captured →  **58,620**
- SHA256 hash →  **f446de335565fb0b0ee5e5a3266703c778b2f3dfad7efeaeccb2da5641a6d6eb**
- Protocol Observed →  **TCP, HTTP, DNS, ARP**  

**Analysis:**  
File metadata provide critical info for SOC investigations:
- Establish the baseline visibility before deeper traffic analysis 
- Validating the authenticity of packet capture 
- Verifying the packet integrity to ensure evidence have not been tampered with.

## 📝Task 3: Packet Dissection  

**Process:**  
	1. Open the capture file in Wireshark  
	2. Navigate to packet 38 using "Go To Packet" function  
	3. Expanded packet details for full dissection  
<img width="1916" height="925" alt="Packet-details" src="https://github.com/user-attachments/assets/ec653912-ed4e-418d-bf69-cf9b4a1678f8" />

**Result:**
- Markup Language used under HTTP Protocol : **eXtensible Markup Language**
- Packet's arrival date : **05/13/2024**
- TTL Value : **47**
- TCP Payload Size: **424 bytes**
- e-Tag value: **9a01a-4696-7e354b00**

**Analysis:**  
Wireshark's layer by layer decoding helps analysts to pinpoint issue within packet such as:  
- Anomalies in TTL that indicates spoofing or misconfigured device
- TCP retransmissions highlight potential instability or incorrect application behavior 

## 📝Task 4: Packet Navigation

**Process:**  
	1. Used "Find Packet" to locate string `r4W` within packet details  
	<img width="1919" height="882" alt="find-packet" src="https://github.com/user-attachments/assets/c8c6bfd6-b680-44ef-9da7-f4af30652dbb" /> <br/>
	3. Exported "HTTP objects" with a text filter applied  
	<img width="1917" height="939" alt="export-object" src="https://github.com/user-attachments/assets/4d18c315-0dfc-47bc-8018-75d63cced2f8" /><br/>
	4. Reviewed the "Expert Information panel" for protocol warnings and errors  
	<img width="1913" height="938" alt="exper-info" src="https://github.com/user-attachments/assets/16434329-ff2b-4a40-89ac-84ff558b5c7f" />


**Result:**  
- Extracted application data → Artist name: **r4w8173**, Alien name: **PACKETMASTER**  
- Expert Information reported → **1,636 warnings**
	
**Analysis:**  
The Expert Information panel consolidates protocol issues by severity (warnings, errors, notes). This feature supports SOC workflows by:    
- Focus on the most impactful issues first  
- Guide remediation efforts by highlighting misconfiguration, retransmission or protocol violations

## 📝Task 5: Packet Filtering
**Process:**  
	1. Applied Wireshark display filter: Hypertext Transfer Protocol on packet **4** to isolate the http traffic  
	2. Verified the number of displayed packets after filtering  
	3. Followed the HTTP stream for packet **33790** to extract application‑level data  

**Result:**  
	• Filter details →Filter query: http, Displayed packet: 1089  
	• Extracted HTTP data → Total no of artis: 3, second artis name: Blad3 
	
**Analysis:**  
Packet filtering helps analysts isolate suspicious traffic for deeper investigation. Additionally, findings such as the extracted artist name demonstrate how application‑level data can support incident investigations and validate anomalies.

## 📝 Key Takeways  
Wireshark commonly used to perform fundamental packet analysis, providing visibility into network traffic and protocol behaviour. Key applications include:  
- Incident investigation → Inspect alerts and help to identify evidence of attack  
- Threat hunting → Detect anomalies and potential of data exfiltration  
- Malware analysis → Identify Indicator of Compromise (IOC) such as malicious IP address, domain name and also extract files, scripts or malicious binaries  

