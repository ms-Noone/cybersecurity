# OverTheWire: Bandit Level 16-20
This walkthrough documents my solutions for the OverTheWire Bandit wargame. Bandit is designed to teach Linux basics, command-line usage, and security concepts.  

## 🔑 Level 16 → Level 17
**Goal:** Retrieve the password of next level by submitting current level password to a port on localhost in range 31000 to 32000
```
ssh -i bandit14_sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

**Steps:**  
1. Login using SSH command above
2. Scan the port range and detect the service/version: `nmap -sV localhost -p 31000-32000`
   - `-sV` → probes open ports to determine service/version information
   <img width="675" height="210" alt="image" src="https://github.com/user-attachments/assets/b8fd5927-4d93-4ebb-ad85-f2f54eddcf1e" />
3. Establish secure connection to the identified port: `ncat --ssl localhost 31790`
5. Paste the password of Level 16 into the ncat session
6. Successful submission reveals SSH Private Key for bandit17

**Analysis:**  
- NMAP is a tool that widely used for discovering open ports and services, Analyst can leverage NMAP to identify outdated or vulnerable services that expand the system's attack surface

**Password for Level 17:**  
No direct password is revealed — instead, you obtain an SSH private key to access bandit17 as in below
<img width="600" height="483" alt="image" src="https://github.com/user-attachments/assets/aa5db7a4-8e42-491b-8533-c13002ef9813" />
