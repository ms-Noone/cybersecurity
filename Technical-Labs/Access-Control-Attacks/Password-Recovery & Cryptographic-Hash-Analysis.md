# Password Recovery & Cryptographic Hash Analysis
**Tools:** Hashcat, John the Ripper (JTR), x2 John Utilities

## 📝 Executive Summary
This lab demonstrates the use of password-cracking tools to audit password strength and recover credentials from various formats. I will utilize a hybrid workflow between John the Ripper(JtR) and Hashcat against few scenario 

## 🛠️ Scenario 1: Cracking Linux Credential
**Goal:** Audit a system's password policy by targeting local Linux user hashes.

**Technical Execution:**  
1. Linux splits user info and hashes info into `/etc/passwd` and `/etc/shadow`. I used `unshadow` tools to combine them into a format JtR can process
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
    
2. In attack command, i did define the format to ensure that JtR didnt waste time trying to guess the hash. You can identify the format to used by using online tools called [Hashed Identifier](https://hashes.com/en/tools/hash_identifier)
   - **Command:** `john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt`

## 🛠️ Scenario 2: Encrypted Archive Analysis
Hashcat cant see inside file format like ZIP files, RAR files, PDF files or SSH keys. In this scenario, I had to utilized x2 John `zip2john` utilities to extract the cryptographic signature 

**Technical Execution:**  
1. Used `zip2john` to extract the hash  
   **Note:** `zip2john` often leaves the filename and some extra metadata in the output. I manually cleaned zip_hash.txt to make sure only the valid hash remained so Hashcat wouldn't error out.
   - **Command:** `zip2john zipfile.zip > zip_hash.txt`
     
2. Once i cleanded the hash, i move to initiate Hashcat command to crack the password
   - **Command:** `hashcat -m 17210 -a 0 secure_hash.txt /usr/share/wordlists/rockyou.txt`
   - Beside hashcat, you can also use JtR to crack the password. Here is the **Command:** `john --wordlist=/usr/share/wordlists/rockyou.txt secure_hash.txt`
  
## Online Password-Cracking Tools
1. [CrackStation](https://crackstation.net/) - Online password hashed cracker
2. [HashID](https://hashes.com/en/tools/hash_identifier) - Hash type identifier
3. [Hash Mode](https://hashcat.net/wiki/doku.php?id=hashcat) - Hash mode identifier
  
## Key Takeways
- The effectiveness of the Dictionary Attack using rockyou.txt list highlights the critical need for password complexity and length to resist automated attacks.
- Unauthorized access to /etc/shadow is a major red flag. SOC teams should monitor for any unauthorized access to this file as it often precedes a full system compromise.
- JtR is a "Swiss Army Knife" for extracting hashes from files, while Hashcat is the gold standard for high-speed cracking due to its GPU support and advanced attack modes.
