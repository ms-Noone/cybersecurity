# Networking Essentials – TryHackMe Walkthrough
	• Date Completed: Dec 29, 2025  
	• Category: Networking  
	• Difficulty: Easy  
	• Estimated Time: ~45 minutes  
	• Focus Areas: WHOIS, DNS, HTTP and FTP, SMTP, POP3 & IMAP  
	• Goal: Strengthen understanding of  core TCP/IP protocols.  

## 📝 Introduction

This room builds on foundational networking concept by exploring how a protocol operates behind the graphical interfaces. The exercise focus on protocol: DNS, HTTP, FTP, SMTP, POP3, and IMAP reinforcing both theoretical knowledge and practical command usage.

## 📝 Task 2: DNS – Remembering Addresses
This task reinforced theoretical knowledge through guided questions and quizzes

**Key Concepts:**  
  - DNS responsible for mapping domain name to an IP address
  - OSI Layer : Application (Layer 7)
  - Transport Protocol : UDP/53, TCP/53
  - DNS Record:
  
    | Record  | Description |
	| ------------- | ------------- |
    | A Record | Map Domain Name to one or more IPv4 address |
	| AAAA Record | Map Domain Name to one or more IPv6 address | 
	| CNAME Record | Map Domain Name to another domain name |
	| MX Record | Specifies mail server responsible for handling email for the Domain|  

**<ins>Command Examples:</ins>**  
- `nslookup <domain_name>`  #Lookup the IP address of a domain

**Reflection:**  
DNS simplifies internet use by mapping domains to IPs, but this convenience creates the attack surface. Mastering DNS concepts are vital for detecting anomalies and defending against hijacking or redirection attacks.

## 📝 Task 3: WHOIS
**Process:**  
  - Ran `whois <domain_name>` to view records of any registered domain
	
**Key Concepts:**  
  - WHOIS record provides information about the entity that registered a domain name, including name, phone number, email, and address
	
**Reflection:**  
WHOIS reveals ownership and contact details of domains, making it useful for investigations and threat analysis, but also a potential privacy concern if data is exposed.

## 📝 Task 4: HTTP(S) – Accessing the web
**Process:**  
  - Used telnet to connect to webserver : `telnet MACHINE_IP 80`
  - Retrieve the hidden flag by accessing the flag.html :  
	`GET /flag.html HTTP/1.1`  
	`Host : Anything`
	
**Key Concepts:**  
  - Transport Protocol : 
	| Protocol  | Transport Protocol | Port Number |
	| ------------- | ------------- | ------------- |	
	| HTTP | TCP | 80 |
	| HTTPS | TCP | 443 |
  - Common Web Methods:
    | Command  | Description |
	| ------------- | ------------- |
	| GET |	Retrieve data from web server |
	| POST | Submit data to server (e.g., forms) |
	| PUT | Create or update resource on server |
	| DELETE | Deletes files or resource from server |
	
**Reflection:**  
HTTP transmits data in clear text, making it easy for attacker to intercepts with tools like Wireshark. HTTPS adds encryption, this help to securing sensitive information during web communication

## 📝 Task 5: FTP - Transferring Files
**Process:**  
  - Ran `ftp MACHINE_IP` to connect to remote FTP server
  - Entered username using `USER <username>`
  - Ran `ls` to list file available to download
  - Ran `RETR <filename>` to download the file from FTP server to client
	
**Key Concepts:**  
  - Transport Protocol : TCP/21
  - Common FTP Commands
    | Command  | Description |
	| ------------- | ------------- |
	| USER | Input username |
	| PASS | Input password |
	| RETR | Download file from FTP Server |
	| STOR | Upload file to FTP Server |

**Reflection:**  
FTP is designed for file transfer but transmits data in clear text, exposing credentials and files to interception. A more secure alternative is SFTP, which adds encryption to protect data in transit.

## 📝 Task 6: SMTP – Sending Email
**Process:**  
  - Connect to Mail Server using : `telnet MACHINE_IP 25`
  - Initiated SMTP Connection : `Helo client.thm`
  - Specifies sender & recipient:
	`MAIL FROM: <sender_email>`
	`RCPT TO: <recipient_email>`
  - Began writing email content : `DATA`
  - Ended the message with a single period `.` to indicate completion.
	
**Key Concepts:**  
  - Simple Mail Transfer Protocol (SMTP) defines how mail client communicate with mail server and how a mail server relay message to each other.
  - Transport Protocol : TCP/25
  - Common SMTP Commands:  
    | Command  | Description |
	| ------------- | ------------- |
	| HELO/EHLO |	Initiate connection with the server |
	| MAIL FROM |	Sender email address |
	| RCPT TO |	Recipient email address |
	| DATA |	Begin composing message body |
	| . |	End of message |
	
	
**Reflection:**  
SMTP enables email delivery between clients and servers, but in its plain form it transmits data unencrypted, exposing messages and credentials to interception. SMTPS is a secure option and essential to protect email confidentiality and integrity.

## 📝 Task 7: POP3 – Receiving Email
**Process:**  
  - Connected to Mail Server using : telnet MACHINE_IP 110
  - Started Authentication : 
	`AUTH`
	`USER <username>`
	`PASS < password>`
  - Requested number of message : `STAT`
  - Listed messages and their size : `LIST`
  - Retrieve the hidden flag by  accessing the fourth message:  
	`RETR 4`
	
**Key Concepts:**  
  - Post Office Protocol v3(POP3) design to allow client to communicate with mail server and download email message
  - Transport Protocol : TCP/110(unencrypted)
  - Common POP3 Commands:
    | Command  | Description |
	| ------------- | ------------- |
	| USER <username> |	Provide username |
	| PASS <password> |	Provide password |
	| STAT |	Show number of messages and total size |
	| LIST |	List messages with size |
	| RETR |	Retrieve a specific message |
	| DELE |	Delete a specific message |
	
	
**Reflection:**  
POP3 enables clients to retrieve email from servers, but in its plain form it exposes credentials and messages to interception. Using POP3S (TCP/995) with SSL/TLS is essential to protect email confidentiality and integrity

## 📝 Task 8: IMAP – Synchronizing Email
This task reinforced theoretical knowledge through guided questions and quizzes

**Key Concepts:**  
  - Internet Message Access Protocol (IMAP) allows clients to access and manage email directly on the server.
  - Transport Protocol : TCP/143
  - IMAP Common Command :
    | Command  | Description |
	| ------------- | ------------- |
	| LOGIN |	Authenticate with username and password |
	| LIST |	Display available mailboxes |
	| SELECT |	Choose a mailbox (e.g., INBOX) |
	| FETCH |	Retrieve specific message content |
	| STORE |	Update message flags (e.g., read/unread |
	| LOGOUT |	End the session |

**Reflection:**  
IMAP enables clients to manage and synchronize emails directly on the server, making it more flexible than POP3. However, in plain form it transmits data unencrypted, so IMAPS (TCP/993) is essential to protect credentials and message confidentiality

## 📝 Closing Reflection
This walkthrough reinforced my understanding of core TCP/IP protocols and their security implications. By practicing hands‑on commands and analysing risks, I strengthened my ability to detect anomalies, validate records, and recommend secure alternatives. These skills directly support SOC analyst responsibilities such as monitoring traffic, identifying misconfigurations, and defending against protocol‑based attacks.

