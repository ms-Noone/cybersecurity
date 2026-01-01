# 🖧 TryHackMe Walkthrough: Networking Concepts

## 📌 Room Overview
	• Difficulty: Easy
	• Estimated Time: ~60 minutes
	• Goal: Build foundational networking knowledge for cybersecurity
	
## 📝 Introduction
This is the first in a series of four room dedicated to introduce user to foundation of networking and most common networking protocol.

### Learning Objective:
	• ISO OSI network model
	• IP addresses, subnets, and routing
	• TCP, UDP, and port numbers
	• How to connect to an open TCP port from the command line

## 📝 Task 2: OSI Model
Open System Interconnection (OSI) model defines a framework for computer network communication. The OSI model is composed of 7 layers, each handling a specific function.

**Key Concepts:**
| Layer Number  | Layer Name | Main Function | Example of Protocol and Standards |
| ------------- | ------------- | ------------- | ------------- |
| Layer 7 | Application Layer | 	Providing services and interfaces to applications  | HTTP, FTP, DNS, POP3, SMTP, IMAP  |
| Layer 6  | Presentation Layer  | Data encoding, encryption, and compression  | Unicode, MIME, JPEG, PNG, MPEG  |
| Layer 5  | Session Layer  | Establishing, maintaining, and synchronising sessions  | NFS, RPC  |
| Layer 4  | Transport Layer | End-to-end communication and data segmentation  | UDP, TCP  |
| Layer 3  | Network Layer  | Logical addressing and routing between networks  | IP, ICMP, IPSec  |
| Layer 2  | Data Link Layer  | Reliable data transfer between adjacent nodes  | Ethernet (802.3), WiFi (802.11)  |
| Layer 1  | Physical Layer  | Physical data transmission media  | Electrical, optical, and wireless signals  |

👉 Mnemonic: _Please Do Not Trust Sale Person Advice_

### Flags/Answers:
	• End-to-end communication → Transport Layer (Layer 4)
	• Routing packets → Network Layer (Layer 3)
	• Encoding application data → Presentation Layer (Layer 6)
	• Same network segment transfer → Data Link Layer (Layer 2)

## 📝 Task 3: TCP/IP Model
TCP/IP Model is a Practical model developed by DoD for Internet use. One of the difference between OSI & TCP/IP model is the application layer in TCP/IP Model encompassed of 3 OSI layers 5–7.

**Key Concepts:**  
- Layers: Physical, Data Link, Network, Transport, Application
	
### Flags/Answers:  
	• HTTP belongs to → Application Layer
	• Application layer covers → 3 OSI layers (5, 6, 7)

## 📝 Task 4: IP Addresses, Subnets & Routing
Every device on a networks need a unique identifier (IP Address) to communicate. By using TCP/IP protocol suite, each device connected to the network will be assign their own IP. Below is the example of IP address:
![alt text](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1719849005781.png)


**Key Concepts:**  
- Router operate at layer 3 (Network Layer), function to forward data packet between network.
- There is 2 Type of IP address:
  - Public IP : Assign by your ISP for internet Access, Globally unique
  - Private IP:  Assign by router, used for communication within your home/ office network  
		Private IP ranges:  
				&emsp;- 10.0.0.0/8  
				&emsp;- 172.16.0.0/12  
				&emsp;- 192.168.0.0/16    
		
**<ins>Command Examples:</ins>**  
- _ifconfig_ or _ipconfig_ : command to show IP address

### Flags/Answers:  
	• Not private → 49.69.147.197
	• Invalid IP → 192.168.305.19

## 📝 Task 5: UDP & TCP
UDP & TCP protocol enable processes on networked host to communicate with each other. UDP doesn’t provide mechanism to know that the packet has been delivered while in TCP, each data has a sequence number that make it easy for receiver to identify lost or duplicated packet. In TCP, they will establish the connection between the two device before the data transfer using Three way Handshake.
![alt text](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1719849036216.svg)


**Key Concepts:**  
	• UDP: Connectionless, fast, no delivery guarantee.  
	• TCP: Connection-oriented, reliable, uses three-way handshake.  
	• Ports range: 1–65535.  
	
### Flags/Answers:  
	• Protocol requiring handshake → TCP
	• Approximate port numbers → 65k

## 📝 Task 6: Encapsulation
Encapsulation refers to the process of data been wrapped layer by layer by adding a header ( and sometime a trailer)
![alt text](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1719849061418.svg)

**Key Concepts:**  
| Layer  | Protocol Data Unit (PDU)  |
| ------------- | ------------- |
| Application Layer  | Data  |
| Transport Layer  | Segment (TCP) / Datagram (UDP)  |
| Network Layer  | Packet (IP)  |
| Data Link Layer  | Frame (Ethernet/WiFi)  |	 
	
### Flags/Answers:  
	• WiFi encapsulation → Frame
	• UDP data unit → Datagram
	• TCP data unit → Segment

## 📝 Task 7: Telnet
Telnet protocol is a network protocol for connect and communicate with a remote system and issue text commands

**Key Concepts:**  
	• Echo server → Port 7  
	• Daytime server → Port 13  
	• Web server → Port 80  
	
**<ins>Command Examples:</ins>**  
_telnet MACHINE_IP 7_  
_telnet MACHINE_IP 13_  
_telnet MACHINE_IP 80_  

### Flags/Answers:  
	• HTTP Server Name & Version : lighttpd/1.4.63
	• Flag: THM{TELNET_MASTER}




