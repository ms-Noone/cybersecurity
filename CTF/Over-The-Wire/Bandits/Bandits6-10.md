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
2. Display contents: `cat /var/lib/dpkg/info/bandit7.password`
3. Output:  
   <img width="675" height="33" alt="image" src="https://github.com/user-attachments/assets/dd892218-da90-4061-81a8-2673572e95d1" />

**Analysis:**  
- File attributes (owner, group, size) are powerful filters that we can use to locate sensitive data in large system
- Metadata awareness helps analysts to quickly triage suspicious files without manually parsing everything

**Password for Level 7:**  
`morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`  _#Passwords shown are from OverTheWire Bandit and reset periodically_
