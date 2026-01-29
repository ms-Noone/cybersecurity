# OverTheWire: Bandit Level 11-15
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

**Analysis:**  
- 

**Password for Level 12:**  
`7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`  _#Passwords shown are from OverTheWire Bandit and reset periodically_

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

**Password for Level 13:**  
`FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn`  _#Passwords shown are from OverTheWire Bandit and reset periodically_

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
6. set strict permission on the private key: `chmod 600 nbandit14_sshkey.private`  
7. ssh using the private key
   - Command: `ssh -i bandit14_sshkey.private bandit14@bandit.labs.overthewire.org -p 2220`
   - Pre-requisite to ssh using private key:  
     a. Public key is added in the remote server  
     b. Private key on local machine must have stric permission  
8. Successful login reveals access to Level 14  

**Analysis:**  
- This challenge demonstrate the importance of key-based authentication in secure system
- Proper file permission and least privilege enforcement are critical to prevent unauthorized access to sensitive key
