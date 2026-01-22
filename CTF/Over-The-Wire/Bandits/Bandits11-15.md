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
