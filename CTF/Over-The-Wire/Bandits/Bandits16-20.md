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

## 🔑 Level 17 → Level 18
**Goal:** Retrieve the password for the next level by reading the only line in `passwords.new` that is not present in `passwords.old`  

**Steps:**  
1. Login to bandit17 using the SSH private key obtained from Level 16
2. list file in the home directory: `ls`
    - Confirmed the presence of `passwords.new` and `passwords.old`
3. Compare and find the difference between the file: `diff passwords.new passwords.old`
   <img width="481" height="81" alt="image" src="https://github.com/user-attachments/assets/a3ec6014-e4d6-4d3d-b034-59c493abb79f" />
4. The output reveals the password to Level 18
5. Login to bandit18:
   ```
   ssh bandit18@bandit.labs.overthewire.org -p 2220
   # password: x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
   ```
6. You will see byebye when trying to login to bandit18

**Analysis:**  
- This challenge demonstrates the importance of change detection - file comparison helps to identify or spot the unauthorized modification or uncover anomalies in log, configuration or datasets

**Password for Level 18:**  
`x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO`#Passwords shown are from OverTheWire Bandit and reset periodically

## 🔑 Level 18 → Level 19
**Goal:** Retrieve the password for the next level in a file _**readme**_ despite restricted login conditions where someone has modified .bashrc to log you out when you log in with SSH  

**Steps:**  
1. Login to bandit18: `ssh bandit18@bandit.labs.overthewire.org -p 2220 -t /bin/sh`
   - `-t /bin/sh` → tell ssh to run pseudo-terminal immediately after connecting instead of default shell configured in .bashrc
2. list file in the directory: `ls`
   - Confirmed the presence of readme file
3. Retrieve the password from readme file: `cat readme`  
   <img width="427" height="36" alt="image" src="https://github.com/user-attachments/assets/e3ad68c5-fb6c-40c1-9328-baec837ebee1" />

**Analysis:**  
- This challenge demonstrates how attacker could leverage .bashrc to restrict or manipulate user interaction on a login shell
- Its also highlight the importance of understanding SSH invocation methods, both for detecting misuse and for maintain legitimate access in restricted environment

**Password for Level 19:**  
`cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8`#Passwords shown are from OverTheWire Bandit and reset periodically

## 🔑 Level 19 → Level 20
**Goal:** Retrieve the password for the next level by using the setuid binary 

**Steps:**  
1. Login to bandit19: `ssh bandit19@bandit.labs.overthewire.org -p 2220`  
2. list file to see the setuid binary in the home directory: `ls -l`  
   - Confirmed that `bandit20-do` have special permission (suid) :
     <img width="574" height="50" alt="image" src="https://github.com/user-attachments/assets/22b750c8-95b9-405c-80e9-20b10ef48230" />
3. list file permission for /etc/bandit_pass/bandit20: `ls -l /etc/bandit_pass/bandit20`
   <img width="596" height="36" alt="image" src="https://github.com/user-attachments/assets/bd52c0ba-de68-4d19-b060-d4a25b91c9c2" />
4. Retrieve password by run the command as bandit20:  
   <img width="528" height="40" alt="image" src="https://github.com/user-attachments/assets/c6376347-cc79-4c4f-9c5d-f85af26daeb7" />

**Password for Level 20:**  
`0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO`#Passwords shown are from OverTheWire Bandit and reset periodically

## 🔑 Level 20 → Level 21
**Goal:** Retrieve the password for the next level by connecting to localhost on the specified port. The service reads a line of text from the connection and compares it to the password from the previous level (bandit20). If the password is correct, it transmits the password for the next level (bandit21).  

**Steps:**  
1. Login to bandit20: `ssh bandit20@bandit.labs.overthewire.org -p 2220`
2. list file to see the setuid binary in the home directory: `ls -l`  
   - Confirmed that `suconnect` is a file with priviledge escalation
3. setup a listener by send it the password of bandit20: `echo -n "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" | ncat -l -p 1234 &`
4. connect to the localhost with the specified port: `suconnect localhost 1234`
5. The service validates the password and returns the password for Level 21
   <img width="790" height="84" alt="image" src="https://github.com/user-attachments/assets/9edc78ea-b096-4a87-95cf-03e2a74f1ac4" />

**Analysis:**  
- This challenge demonstrate the basic of setting up listener and handling simple client-server communication.
- It also highlight the importance of carefully designing SUID program and network service since improper handling may leak sensitive information or enable priviledge escalation

**Password for Level 21:**  
`EeoULMCra2q0dSkYj561DX7s1CpBuOBt`#Passwords shown are from OverTheWire Bandit and reset periodically
 
