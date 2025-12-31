## 📌 Room Overview
	• Difficulty: Easy
	• Estimated Time: ~60 minutes
	• Focus Areas: DHCP, ARP, ICMP, Routing, NAT
	• Goal: Understand essential networking protocols and how they support communication across networks.

## 📝 Introduction  
Networking Essentials builds on Networking Concepts, focusing on protocols that make communication possible.  
### Learning Objective
	• Dynamic Host Configuration Protocol (DHCP)
	• Address Resolution Protocol (ARP)
	• Network Address Translation (NAT)
	• Internet Control Message Protocol (ICMP)
		○ Ping
		○ Traceroute

## 📝 Task 2: DHCP – Give Me My Network Settings
Dynamic Host Configuration Protocol (DHCP) automatically assigns IP addresses and network settings.

**Key Concepts:**  
- DORA (Discover -> Offer -> Request -> Acknowledge) Steps
  ![alt text](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1719849148646.svg)
- Dynamic IP : IP address automatically from DHCP server
- Static IP : IP address manually assign from DHCP server

### Flags/Answers:  
	• DORA Steps → 4
	• Destination IP address used to send DHCP Discover Packet → 255.255.255.255
	• IP address use to get IP network configuration over DHCP → 0.0.0.0

## 📝 Task 3: ARP – Bridging Layer 3 to Layer 2
ARP (Address Resolution Protocol) maps IP addresses (Layer 3) to MAC addresses (Layer 2).

**Key Concepts:**  
- ARP request : “Who has IP X?”
- ARP reply : “MAC address Y has IP X.”
- ARP Cache : table stored in device's memory that map IP address to their corresponding MAC Address. This is to speed up communication on a local network by avoiding repeated ARP request
	
**<ins>Command Examples:</ins>**  
- _arp -a_          # View ARP Cache table
- _ip neigh show_   # Linux equivalent
- _arp -s <IP Address> <Mac Address>_  #Manually enter static ARP

### Flags/Answers:  
	• Destination MAC Adress used in ARP Request → ff:ff:ff:ff:ff:ff
	• Mac Address of 192.168.66.1 → 44:df:65:d8:fe:6c

## 📝 Task 4: ICMP – Troubleshooting Networks
ICMP (Internet Control Message Protocol) is used for network diagnostics and error reporting

**Key Concepts:**  
- Command :
   - Ping = Test connectivity to a target system and measure the round trip time( RTT)
   - Traceroute / tracert = Discover the route of data packet from your host to the target
		
- ICMP messages: Echo Request (ICMP Type 8) / Reply (ICMP Type 0)
- Time To Live (TTL) : maximum number of routers a packet can travel through before its dropped.
	
**<ins>Command Examples:</ins>**  
- _ping <IP>_ #To test connectivity  
- _traceroute google.com_   # Linux command  
- _tracert google.com_      # Windows command  
- _tracert -h <TTL> <IP>_ #To set TTL  

### Flags/Answers:  
	• Bytes sent → 40
	• traceroute filed that require to become zero → TTL

## 📝 Task 5: Routing
Routing directs packets between networks using Routing table

**Key Concepts:**
- Routing Table : File that contains a set of rule that show information on what path a data packet took to the destination
- Routing Protocol :
   - OSPF (Open Shortest Path First) → Link‑state protocol where routers exchange information about their connected links and calculate the most efficient path using Dijkstra’s algorithm.
   - EIGRP (Enhanced Interior Gateway Routing Protocol) → Cisco proprietary hybrid protocol that combines distance‑vector and link‑state concepts. It uses metrics like bandwidth and delay (not just bandwidth) to choose the best path.
   - BGP (Border Gateway Protocol) → The primary exterior gateway protocol of the internet. It ensures data is routed efficiently across multiple autonomous systems (networks). 
- RIP (Routing Information Protocol) → A distance‑vector protocol used in small networks. It relies on hop count as its metric (not link‑state). 
		
### Flags/Answers:  
	• Cisco property routing Protocol → EIGRP
	
## 📝 Task 6: NAT
NAT (Network Address Translation) service used in router to translate private IP to Public IP
![alt text](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1719849362861.svg)  

**Key Concepts:**  
- Static NAT : Permanently maps one private IP to one public IP.
- Dynamic NAT : Temporarily assigns a public IP from a pool to a private IP, changing as sessions occur.
	
### Flags/Answers: 
	• Phone Public IP when accessing the internet → 212.3.4.5
	• Total simultaneous TCP connection can it maintain → 65K

## 📝 Task 7: Closing Notes
### Flags/Answers: 
	• Flag →THM{computer_is_happy}

