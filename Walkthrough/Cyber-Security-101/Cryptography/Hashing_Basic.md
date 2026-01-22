# Hashing Basic – TryHackMe Walkthrough 

**Room** : Hashing Basic  
**Date Completed** : Jan 22, 2026  
**Category** : Cryptography  

**Objective:**
Explore on Hashing functions and their uses in password verification and file integrity checking. 

# Task 2: Hash Function
**Key Takeaways:** 
  - Hashing helps to protect data's integrity and ensure password's confidentiality
  - Hash collision occurs when two different input produce the same output
  - Hash security relies on one way transformation (hard to reverse) and collision resistance

**Security Perspective:**  
  - Weak hashesh (MD5, SHA1) increase hash collision risk, making them easier to exploit
  - Use SIEM rules to flag application that still relying on MD5 / SHA1

# Task 3: Insecure Password Storage for Authentication
**Key Takeaways:** 
  - Common Insecure practice: storing password in plaintext, using deprecated encryption and rely on weak hashing algorithm
  - **Password salting:** Adding a random value to the password before it hashing to strengthen resistance against rainbow table attacks

**Security Perspective:** 
  - Always pair hashing + salting + modern hash algorithm to resist brute force
  - Weak hashesh increase the risk of data breach, ex: Adobe's and Linkedin incident due to insecure password storage
  - **Best practice:** Enforce password policies that mandate salting and strong hashing

# Task 4: Using Hashing for Secure Password Storage
**Key Takeaways:** 
  - **Rainbow table:** a lookup table mapping hashes to plaintexts
  - Online rainbow table: CrackStation and Hashes.com
  - Password salting is randomly generated and unique per user

**Security Perspective:** 
  - Using unique salt per user prevent attackers from reusing rainbow table across multiple account
  - Use SIEM to flag system using unsalted or weak hashes as this represent high-risk authentication practice

# Task 5: Recognising Password Hashes
**Key Takeaways:** 
  - Linux Password: stored in /etc/shadow and only readable to root user
  - Windows Password: stored in Security Account Manager(SAM) typically using NTLM hashing
    
**Security Perspective:** 
  - Restricted access to the password storage file to prevent credential theft
  - NTLM are vulnerable to offline cracking, recommended to use stronger authentication mechanism like kerberos

# Task 6: Passwrod Cracking
  - **Hash Cracking Tools:** Hashcat, John the Ripper, Rainbow Table  
**Process:**
  - **Command:**  `hashcat -m <hash_type> -a <attack_mode> hashfile wordlist #to crack the hash`
  - Run hashcat command: `hashcat -m 3200 -a 0 Hashing-Basics/Task-6/hash1.txt /usr/share/wordlists/rockyou.txt`
    <img width="816" height="825" alt="image" src="https://github.com/user-attachments/assets/f275c950-aa06-4c51-bfc3-33cda955a7f4" />
  - Run hashcat command: `hashcat -m 1400 -a 0 Hashing-Basics/Task-6/hash2.txt /usr/share/wordlists/rockyou.txt`
    <img width="858" height="579" alt="image" src="https://github.com/user-attachments/assets/8dac5f56-cfe8-4424-b429-94c4c2909d41" />
  - Run hashcat command: 


    
**Result:**
  - bcrypt hash cracked → 85208520
  - SHA-256 hash cracked → halloween
  - SHA-512crypt hash cracked → spaceman
  - MD5 hash cracked → funforyou
    
**Analysis:**
