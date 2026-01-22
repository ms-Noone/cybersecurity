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
**Goal:** Retrieve the password stored in `data.txt` where the file is compressed multiple time using different formats

**Steps:** 
  - The solution steps will be separated into 3 main task: Setting up temporary directory, revert hexdump and decompressing

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
1. convert hexdump back into its original binary format: `xdd -r hexdump_data compress_data`  
   xdd : Command-line tool to create / reverts hexdump file, enable file inspection, debugging, binary patching or ROM hacking
   -r : Converts a hex dump back into its original binary format

<ins>**_Decompress File_**</ins>
1. Inspect the file type: `file compress_data` to reveals compression format
   <img width="1243" height="36" alt="image" src="https://github.com/user-attachments/assets/78a6a86a-0362-4c7a-88b5-dbd6ee84620a" />

2. Iteratively decompress until the original password file is revealed:
   - if gzip:
   - if bzip2:
   - If tar file:

3. Repeat file and decompression until you reach a plain text file
4. Display final password:

**Analysis:**  
- 

**Password for Level 12:**  
``  _#Passwords shown are from OverTheWire Bandit and reset periodically_
