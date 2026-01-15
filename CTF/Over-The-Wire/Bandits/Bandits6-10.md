# OverTheWire: Bandit Level 6-10
This walkthrough documents my solutions for the OverTheWire Bandit wargame. Bandit is designed to teach Linux basics, command-line usage, and security concepts.  

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

**Password for Level 7:**  
`morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`  _#Passwords shown are from OverTheWire Bandit and reset periodically_

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

**Password for Level 8:**  
`dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`  _#Passwords shown are from OverTheWire Bandit and reset periodically_

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

**Password for Level 9:**  
`4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`  _#Passwords shown are from OverTheWire Bandit and reset periodically_
