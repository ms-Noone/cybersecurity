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
    - `unshadow` command: `unshadow local_passwd local_shadow > unshadowed.txt`
    
2. Initiate John and feed the `unshadow` output to crack the password
