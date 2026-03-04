# OverTheWire: Bandit Level 0-10
This walkthrough documents my solutions for the OverTheWire Bandit wargame. Bandit is designed to teach Linux basics, command-line usage, and security concepts.  

## 🔑 Level 0 → Level 1
**Goal:** Retrieve the password for the next level.  
**Connection:**  
```
ssh bandit0@bandit.labs.overthewire.org -p 2220
# password: bandit0
```
**Steps:**  
1. After login, verify current directory: `pwd`
2. If confirm in /home/bandit0, list files: `ls`
3. Else, change directory to home: `cd ~` then list files `ls`
4. `readme` file is listed in the home directory
5. Display contents: `cat readme`
6. Output:  
   <img width="722" height="134" alt="image" src="https://github.com/user-attachments/assets/ae6b8b1c-55a8-4c9a-aa65-003cf45afb6c" />

**Analysis:**  
- Password stored in basic simple text file
- This challenge highlights the importance of confirming directory context before accessing files

## 🔑 Level 1 → Level 2
**Goal:** Password stored in a file called `-`  
**Steps:**  
1. After login, verify current directory: `pwd`
2. If confirm in /home/bandit0, list files: `ls`
3. Else, change directory to home: `cd ~` then list files `ls`
4. `-` file is listed in home directory
5. Display contents: `cat ./-`
6. Output:  
   <img width="644" height="61" alt="image" src="https://github.com/user-attachments/assets/eaf2b820-0f6a-45f5-a56a-c3f6587e705c" />

**Analysis:**  
- Dashed filename caused command-line confusion and will also break the automation script if not handled properly
- This challenge show that edge case must be handled properly as it can cause unexpected issue

## 🔑 Level 2 → Level 3
**Goal:** Password stored in a file name `--spaces in this filename--`  
**Steps:**  
1. After login, verify current directory: `pwd`
2. If confirm in /home/bandit0, list files: `ls`
3. Else, change directory to home: `cd ~` then list files `ls`
4. `--spaces in this filename--` file is listed in home directory
5. Display contents: `cat ./"--spaces in this filename--"`
6. Output:  
   <img width="698" height="87" alt="image" src="https://github.com/user-attachments/assets/478ee589-9b68-4581-b655-3607d8665600" />

**Analysis:**  
- Spaces in filename cause command execution and automation script to break, they also lead to broken filepath in Web/URL
- Users, developers or analyst should avoid special character in filename as command may interpret them as multiple separate arguments

## 🔑 Level 3 → Level 4
**Goal:** Password stored in a hidden file in `inhere` directory  
**Steps:**  
1. After login, change directory: `cd inhere`
2. List hidden files: `ls -a`
3. `...Hiding-From-You` file is listed
4. Display contents: `cat ...Hiding-From-You`
5. Output:  
   <img width="747" height="92" alt="image" src="https://github.com/user-attachments/assets/2a60a658-b21b-493d-be88-00883c1f1f81" />

**Analysis:**  
- Hidden file used by attacker to obscured data and evade detection by users and security tools
- For analyst, thorought enumeration is critical to avoid missing hidden files, as this may lead to incomplete investigation

## 🔑 Level 4 → Level 5
**Goal:** The password for the next level is stored in a file inside the `inhere` directory, but the file is human‑readable among many binary files  
**Steps:**  
1. After login, change directory: `cd inhere`  
2. Find the human-readable file: `file ./-file0*`  
   <img width="464" height="179" alt="image" src="https://github.com/user-attachments/assets/99279eba-9ff4-4d33-9907-8e856de5a8f2" />
3. Display contents: `cat ./-file07`
4. Output:  
   <img width="461" height="31" alt="image" src="https://github.com/user-attachments/assets/c01c56b3-3baf-4d8e-8164-78f8be9e776d" />

**Analysis:**  
- `file` tool helps analyst to quickly classify data and avoid wasting time parsing irrelevant files during investigation  

## 🔑 Level 5 → Level 6
**Goal:** The password for the next level is stored in a file inside the `inhere` directory. The file is the only one that is human‑readable, 1033 bytes in size, and not executable

**Steps:**  
1. After login, change directory: `cd inhere`  
2. Find human-readable file with 1033bytes size and not executable: `find maybehere* -size 1033c ! -executable`  
   <img width="699" height="36" alt="image" src="https://github.com/user-attachments/assets/f295b97f-ab93-44dc-a419-a620dc6c9d9c" />
4. Display content: `cat maybehere07/.file2`  
6. Output:  
   <img width="557" height="41" alt="image" src="https://github.com/user-attachments/assets/6d079e0c-9fd7-4570-8271-2d92a42d115f" />

**Analysis:**  
- This challenge highlight the needs of combining multiple checks (file type + content) to filter noise and focus on relevant data  
- Analysts must pay attention to ambiguous files with unusual sizes, as they may indicate attacker activity or data exfiltration attempts  

## 🔑 Level 6 → Level 7
**Goal:** Retrieve the password stored in file owned by bandit7 and group bandit6 with file size of 33bytes
**Connection:**  
```
ssh bandit6@bandit.labs.overthewire.org -p 2220
# password: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```
**Steps:**  
1. After login, retrieve the file: `find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null`  
   - `-type f` → look only for files  
   - `-user` → owned by user  
   - `-group` → belong to group  
   - `2>/dev/null` → hide error message like 'Permission denied'  
2. Display contents: `cat /var/lib/dpkg/info/bandit7.password`
4. Output:  
   <img width="675" height="33" alt="image" src="https://github.com/user-attachments/assets/dd892218-da90-4061-81a8-2673572e95d1" />

**Analysis:**  
- File attributes (owner, group, size) are powerful filters that we can use to locate sensitive data in large system
- Metadata awareness helps to quickly triage suspicious files without manually parsing everything

## 🔑 Level 7 → Level 8
**Goal:** Retrieve the password stored in a file called `data.txt` and find the line containing the word `millionth`  

**Steps:**  
1. After login, list file: `ls`  
2. `data.txt` is listed in the home directory 
3. search for target string in data.txt: `grep 'millionth' data.txt`  
4. Output:  
   <img width="453" height="34" alt="image" src="https://github.com/user-attachments/assets/61e08408-33bf-4e4a-a9cc-ee553aa64c67" />

**Analysis:**  
- `grep` is a essential utility in log analysis. Ex: Detecting suspicious behaviour like multiple SSH failure
- Beyond simple searches, `grep` is capable of performing complex pattern matching and data extraction

## 🔑 Level 8 → Level 9
**Goal:** Retrieve the password stored in `data.txt` where one line is the only unique entry  

**Steps:**  
1. After login, list file: `ls`  
2. `data.txt` is listed in the home directory 
3. sort and find the unique entry in data.txt: `sort data.txt | uniq -u`  
   - `sort` → sort uppercase followed by lowercase  
   - `uniq -u` → display only unique line
5. Output:  
   <img width="455" height="33" alt="image" src="https://github.com/user-attachments/assets/d125e7dd-f4ca-4007-83b7-505f52047f96" />

**Analysis:**  
- Using `sort` and `uniq` flag reinforced the importance of pattern recognition.
- In log analysis or investigations, anomalies usually hidden in a flood of normal activity. This technique helps to quickly spot the suspicious activities

## 🔑 Level 9 → Level 10
**Goal:** Retrieve the password stored in `data.txt` where the password is human readable preceded by several '=' characters

**Steps:**  
1. After login, list file: `ls`  
2. `data.txt` is listed in the home directory 
3. Extract human readable strings and filter for line containing '=': `strings data.txt | grep "=="`  
   - `strings` → extracts printable text from binary or object file  
5. Output:  
   <img width="401" height="82" alt="image" src="https://github.com/user-attachments/assets/f5c28f61-ea0c-499b-8bb0-4e91c0ead04d" />

**Analysis:**  
- Combining `strings` and `grep` is an effective technique for extracting hidden data from noisy or obfuscated data

**Password for Level 10:**  
`FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey`  _#Passwords shown are from OverTheWire Bandit and reset periodically_

## 🔑 Level 10 → Level 11
**Goal:** Retrieve the password stored in `data.txt` where the password is encoded in base64

**Steps:**  
1. After login, list file: `ls`  
2. `data.txt` is listed in the home directory 
3. Decode the base64 string to reveal the password: `base64 -d data.txt`  
   - `base64 -d` → decodes the encoded text back into human-readable text
5. Output:  
   <img width="403" height="33" alt="image" src="https://github.com/user-attachments/assets/d2059b3f-0b22-4958-88bd-df95e913b9c3" />

**Analysis:**  
- This challenge reinforce the importance of recognizing encoding pattern and applying the right decoding tools to uncover hidden information
