# Wireshark -Tryhackme Walkthrough

Room : [Wireshark The Basic](https://tryhackme.com/room/wiresharkthebasics)  
Date Completed: Jan 7, 2025  
Category: Networking  
Focus Areas: Wireshark  

## 📝 Overview  

Hands-on lab focused on Wireshark fundamentals:  
- Navigate and configure Wireshark interface
- Inspect packet to discover information
- Apply display filter to isolate relevant traffic.
  
**Objective:**  
Practice network analysis and strengthen understanding of protocols within the packet capture. These skills are critical in SOC workflows for detecting anomalies, investigating suspicious traffic, and validating security events.  

## 📝 Task 2: Tool Overview

**Packet file used:**  
- Exercise.pcapng
  
**Process:**  
	1. Open "Exercise.pcapng" in Wireshark  
	2. View file details via "Capture File Properties" located on the bottom left  
  
<img width="1916" height="966" alt="File-Properties" src="https://github.com/user-attachments/assets/346a82c1-47b6-44f6-8eda-7e21bebd0ade" /><br />

**Result:**  
- Flag located under file comment : **TryHackMe_Wireshark_Demo**
- Total Packet captured: **58,620**
- SHA256 hash of Exercise.pcapng : **f446de335565fb0b0ee5e5a3266703c778b2f3dfad7efeaeccb2da5641a6d6eb**
- Protocol Observed : **TCP, HTTP, DNS, ARP**  

**Analysis:**  
Wireshark allows analyst to read and investigate packet in depth. File metadata is vital for:
- Establish the baseline visibility before deeper traffic analysis 
- Validating the authenticity of packet capture 
- Verifying the packet integrity to ensure evidence have not been tampered with.

## 📝Task 3: Packet Dissection  

**Packet file used:**  
- Exercise.pcapng

**Process:**  
	1. Open "Exercise.pcapng" in Wireshark
	2. Navigate to "Go To" > "Go To Packet" > 38
	3. Select the packet to view packet dissection
<img width="1916" height="925" alt="Packet-details" src="https://github.com/user-attachments/assets/ec653912-ed4e-418d-bf69-cf9b4a1678f8" />

**Result:**
- Markup Language used under HTTP Protocol : eXtensible Markup Language
- Packet's arrival date : 05/13/2024
- TTL Value : 47
- TCP Payload Size: 424 bytes
- e-Tag value: 9a01a-4696-7e354b00

**Analysis:**  
Wireshark performs layer by layer decoding which helps analysts to pinpoint issue within packet such as:  
- Anomalies in TTL that indicates spoofing or misconfigured device
- TCP retransmission or incorrect application behavior in Protocol Dissection

