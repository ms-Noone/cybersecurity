# OverTheWire: Bandit Intermediate Level 11-20
This walkthrough documents my solutions for the OverTheWire Bandit wargame. Bandit is designed to teach Linux basics, command-line usage, and security concepts.  

## 🔑 Level 11 → Level 12
**Goal:** Retrieve the password stored in `data.txt` where the password is encoded with ROT13
```
ssh bandit11@bandit.labs.overthewire.org -p 2220
# password: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

**Steps:**  
1. After login, list file: `ls`  
2. `data.txt` is listed in the home directory 
3. Decode the ROT13 strings: `cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'`  
   - `tr` → translate command
   - `A-Za-z` → matches all uppercase and lowecase letter
   - `N-ZA-Mn-za-m` → shift each letter by 13 places
5. Output:  
   <img width="537" height="33" alt="image" src="https://github.com/user-attachments/assets/6e7191d4-aa63-4805-bd23-95ae2faaedf7" />

## 🔑 Level 12 → Level 13
**Goal:** Retrieve the password stored in `data.txt` where the file is compressed multiple times using different formats

**Steps:** 
  - The solution steps will be divided into 3 main task: Setting up a temporary directory, revert the hexdump and decompressing the file

<ins>**_Setting Up Temporary Directory_**</ins>
    
1. After login, list file: `ls`  
2. `data.txt` is listed in the home directory
3. copy the file to temporary working directory:
   ```
   mktemp -d #to create directory using hard to guess name
   cp ~/data.txt .
   mv data.txt hexdump_data
   ```
<ins>**_Revert Hexdump File_**</ins>
1. convert hexdump back into its original binary format: `xxd -r hexdump_data compress_data`  
   xxd : Command-line tool to create / reverts hexdump file, useful for inspection and debugging
   -r : Converts a hex dump back into its original binary format

<ins>**_Decompress File_**</ins>
1. Inspect the file type: `file compress_data` to reveals compression format
   <img width="1261" height="56" alt="image" src="https://github.com/user-attachments/assets/a36a101b-520e-4b4d-92f0-bafbef997847" />

2. Iteratively decompress until the original password file is revealed:
   - if gzip:
     ```
     mv compress_data compress_data.gz
     gzip -d compress_data.gz
     ```
   - if bzip2:
     ```
     mv compress_data compress_data.bz2
     bzip2 -d compress_data.gz
     ```
   - If tar file:
     ```
     mv compress_data compress_data.tar
     tar -xf compress_data.gz
     ```

3. Repeat `file` inspection and decompression until you reach a plain text file
4. Display final password:  
   <img width="486" height="54" alt="image" src="https://github.com/user-attachments/assets/38a757cb-12dd-42e1-ba93-356781165ee3" />

**Analysis:**  
- Knowing how to peel back each layer in file inspection is critical for uncovering the hidden data

## 🔑 Level 13 → Level 14
**Goal:** Retrieve the password for the next level by using the SSH private key stored in the home directory  

**Steps:**  
1. After login, list file: `ls`  
2. `sshkey.private` is listed in the home directory
3. copy the content of `sshkey.private`
4. exit ssh and create file `bandit14_sshkey.private` on your local machine
   ```
   exit
   vim bandit14_sshkey.private
   ```
5. Paste content copied in step 3 into `bandit14_sshkey.private`
6. set strict permission on the private key: `chmod 600 bandit14_sshkey.private`  
7. ssh using the private key
   - Command: `ssh -i bandit14_sshkey.private bandit14@bandit.labs.overthewire.org -p 2220`
   - Pre-requisite to ssh using private key:  
     a. Public key is added in the remote server  
     b. Private key on local machine must have stric permission  
8. Successful login reveals access to Level 14  

**Analysis:**  
- This challenge demonstrate the importance of key-based authentication in secure system
- Proper file permission and least privilege enforcement are critical to prevent unauthorized access to sensitive key

## 🔑 Level 14 → Level 15
**Goal:** Retrieve the password for the next level by submitting the current level password to port 30000 on localhost

**Steps:**
1. Login to bandit14: `ssh -i bandit14_sshkey.private bandit14@bandit.labs.overthewire.org -p 2220`
2. get the password for bandit14: `cat /etc/bandit_pass/bandit14`
3. Establish connection to localhost: `nc localhost 30000`
4. paste the password from steps 2 into the netcat session
5. Successful reveals password to Level 15

**Analysis:**  
- Netcat operates on both listen and connect mode, in this challenge it is used in connect mode to establish a client session with localhost
- Netcat does not support TL/SSL encryption, for secure encrypted communication will require other tools such as `ncat` and `openssl`
- Attacker might misuse Netcat to create a backdoors, therefore it is important to monitor any unusual network activity and investigate suspicious connection

## 🔑 Level 15 → Level 16
**Goal:** Retrieve the password for the next level by submitting the current level password to port 30000 on localhost using SSL/TLS encryption

**Steps:**
1. Login to bandit14: `ssh -i bandit14_sshkey.private bandit14@bandit.labs.overthewire.org -p 2220`
2. Establish connection using SSL/TLS encryption: `ncat --ssl localhost 30001`
   - `-ssl` → enables SSL/TLS encryption for the connection
4. paste the password for Level 15 into the ncat session

**Analysis:**  
- Unlike netcat, ncat support TLS/SSL encryption making it suitable for secure communication
- Using encrypted channel is critical to prevent sensitive data from being transmitted in plain text, which attacker can intercept easily

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


