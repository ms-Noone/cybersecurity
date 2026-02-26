# Password Recovery & Cryptographic Hash Analysis
**Tools:** Hashcat, John the Ripper (JTR), x2 John Utilities

## 📝 Executive Summary
This lab demonstrates the use of password-cracking tools to audit password strength and recover credentials from various formats. I will utilize a hybrid workflow between John the Ripper(JtR) and Hashcat against few scenario 

## 🛠️ Scenario 1: Cracking Linux Credential
**Technical Execution:**  
1. Used `unshadow` tools to combine `/etc/shadow` with `/etc/passwd` into a format JtR can process
   - Example files used in this scenario:  
     - **File 1** - local_passwd, contains the `/etc/passwd` line for the root user:
       ```
       root:x:0:0::/root:/bin/bash
       ```
     - **File 2** - local_shadow, contains the `/etc/shadow` line for the root user:
       ```
       root:$6$2nwjN454g.dv4HN/$m9Z/r2xVfweYVkrr.v5Ft8Ws3/YYksfNwq96UL1FX0OJjY1L6l.DS3KEVsZ9rOVLB/ldTeEL/OIhJZ4GMFMGA0:18576::::::
       ```
    - **Command:** `unshadow local_passwd local_shadow > unshadowed.txt`
    
2. Initiate John and feed the `unshadow` output to crack the password
   - **Command:** `john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt`

## 🛠️ Scenario 2: Encrypted Archive Analysis
Hashcat cannot directly read or open file format like ZIP files, PDF files or SSH keys. In this scenario, I utilized x2 John `zip2john` utilities to extract the hash into a text format  

**Technical Execution:**  
1. Used `zip2john` to extract the hash
   - **Command:** `zip2john zipfile.zip > zip_hash.txt`
     
2. Initiate Hashcat and feed the extract text to crack the password
   - **Command:**
  
## 🛠️ Scenario 3: High-Volume Cracking

## Key Takeaways & Security Remediation
