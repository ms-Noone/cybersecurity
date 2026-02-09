# John The Ripper Basic – TryHackMe Walkthrough 

**Room**: John The Ripper Basic  
**Date Completed**: Jan 29, 2026   
**Category**: Cryptography   

**Objective:**  
Explore how to use John The Ripper, a powerful and adaptable hash‑cracking tool.Learn practical techniques to crack:  
- Windows password hashes
- Linux password hashes
- Password‑protected ZIP and RAR files
- Encrypted SSH keys

## Task 3: Setting Up Your System
**Process:**  
1. Installation
   - **Kali Linux:** John pre-installed by default
   - **Other Linux Distribution:** Run command `sudo apt install john`
   - **Windows:** Download and install the zipped binary [here](https://www.openwall.com/john/k/john-1.9.0-jumbo-1-win64.zip)
2. Wordlists
   - wordlist used by John to attempt to pasword guess against targetted service
   - **Default location:** /usr/share/wordlist
   - If not exist, you can get the rockyou.txt wordlist by run command `sudo apt install wordlists`

**Security Perspective:**
- Wordlist like **Rockyou.txt** are built from real breached password, making it valuable for auditing password strength and policy enforcement
- Attacker usually rely on precompiled wordlist to crack the weak password easily,this highlights the importance of password complexity, uniqueness and length to resist dictionary attack

## Task 4: Cracking Basic Hashes
- **Command:** `john --format=[format] --wordlist=[path to wordlist] [path to file]` 
   - `--wordlist=`: specifies using wordlist mode
   - `[path to wordlist]`: path to the wordlist we're using
   - `[path to file]`: path to the file contain password to hash
   - `--format=`: specifies use the format to crack
   - `[format]`: format the hash is in
- Hash Identifier Tool: 
   - Online Tool: [Hash Type Identifier](https://hashes.com/en/tools/hash_identifier)
   - Python Tool: [Hash-identifier](http://gitlab.com/kalilinux/packages/hash-identifier/-/tree/kali/master)
- Online Hash Cracker: [CrackStation](https://crackstation.net/)
     
**Process:**  
1. Q1:
   - Run command `python hash-id.py`
   - Paste hash1.txt to identify the format
     <img width="889" height="349" alt="image" src="https://github.com/user-attachments/assets/8f5ba671-415e-49e3-a03b-360948c36442" /></br>
   - Crack value of hash1.txt: `john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash1.txt`
     <img width="1153" height="162" alt="image" src="https://github.com/user-attachments/assets/5a3d7ed7-2936-4635-a38d-47c050af21fc" />
2. Q2:
   - Identify hash2.txt format  
     <img width="578" height="60" alt="image" src="https://github.com/user-attachments/assets/f3857495-3211-4830-9f8a-77f25609d0bd" />
   - Crack value of hash2.txt: `john --format=raw-sha1 --wordlist=/usr/share/wordlists/rockyou.txt hash2.txt`
     <img width="1124" height="162" alt="image" src="https://github.com/user-attachments/assets/97d9e14d-cd5e-40d5-b39b-5f6c946c3da7" />
3. Q3:
   - Identify hash3.txt format  
     <img width="723" height="27" alt="image" src="https://github.com/user-attachments/assets/d2a046ef-0aba-49b2-8869-5cba31f6dc05" />
   - Crack value of hash3.txt: `john --format=raw-sha256 --wordlist=/usr/share/wordlists/rockyou.txt hash3.txt`
     <img width="1119" height="176" alt="image" src="https://github.com/user-attachments/assets/c496b1b7-5b2f-4a3b-b556-111ea8567ddc" />
4. Q4:
   - Identify hash4.txt format  
     <img width="1177" height="20" alt="image" src="https://github.com/user-attachments/assets/56b7d5a7-03e1-4963-81fd-10588788b062" />
   - Crack value of hash4.txt: `john --format=whirlpool --wordlist=/usr/share/wordlists/rockyou.txt hash4.txt`
     <img width="1130" height="161" alt="image" src="https://github.com/user-attachments/assets/4b78643b-5060-4b11-96cc-7fde3e292c76" />

**Security Perspective:**
- Unsalted weak password reduce security and easily cracked via online rainbow table
- This screenshot demonstrates how quickly such hashes can be broken:
  <img width="1032" height="159" alt="image" src="https://github.com/user-attachments/assets/79e4998c-b0c4-4da6-b854-808d05a1324b" />

## Task 5 - Cracking Windows Authentication Hashes
**Key Takeaways:** 
  - **NThash (NTLM)** : Hash format modern Windows used to stores user and service password
  - **Security Account Manager (SAM)** : Store account information, including usernames and hashed passwords

**Process:**  
1. Crack value of ntlm.txt: `john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt ntlm.txt`
   <img width="1038" height="178" alt="image" src="https://github.com/user-attachments/assets/e32193b9-becb-462a-b73d-49c293f0a767" />

## Task 6: Cracking Hashes from /etc/shadow
**Key Takeaways:** 
- `/etc/shadow` : Linux file where password hashes are stored and only accessible by root user
- Combine `/etc/shadow` and `/etc/password` to unshadow the hashes
- **Command**:  `unshadow [path_to_passwd] [path_to_shadow] > unshadowed.txt`
     - `unshadow` : Invoke the unshadow tool
     - `path_to_password` : file contains copy of /etc/password file
     - `path_to_shadow` : file contains copy to the /etc/shadow file
     
**Process:** 
1. Crack value of etchashes.txt: `john local_passwd etc_hashes.txt`
   <img width="820" height="258" alt="image" src="https://github.com/user-attachments/assets/61c60492-b007-4f9f-bfda-437b5b172f5d" />

**Security Perspective:**
- Unauthorized access to /etc/shadow indicates potential priviledge escalation. SOC teams should monitor for any suspicious root activity and unauthorized file access

## Task 7: Single Crack Mode
**Key Takeaways:** 
- Single Crack Mode is a targeted, context-aware cracking strategy that leverages usernames to guess passwords quickly.
- **Mangling Rule**: John build the dictionary by mangle the password into variations that mimic how real user creates passwords
- **GECOS**: John can also take the GECOS field details and add to wordlist to crack the hashes in single crack mode
- **Command"": `john --single --format=[format] [path to file]`
   - `--single` : Use single hash cracking mode

**Process:**
1. Prepend the hash07.txt with username `Joker`
   - From `7bf6d9bb82bed1302f331fc6b816aada`
   - To `Joker:7bf6d9bb82bed1302f331fc6b816aada`
2. Crack the value of hash07.txt : `john --single --format=Raw-MD5 hash07.txt`
   <img width="807" height="178" alt="image" src="https://github.com/user-attachments/assets/fc02c311-9827-4e2d-86f6-79c1d79bffed" />

**Security Perspective:**
- Enforce password policy that prohibit username-based password and encourage complexities

## Task 8: Custom Rules






