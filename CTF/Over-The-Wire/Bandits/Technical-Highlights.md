# OverTheWire: Bandit — Technical Highlights & Security Analysis
While completing the Bandit series, i selected few level that highlight and demonstrated my proficiency in Linux system administration, vulnerability analysis and custom tool development

## Level 11
**Goal:** Retrieve the password stored in `data.txt`. The password was obfuscated using ROT13, which rotates each letter by 13 positions
```
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

**Steps:**  
1. After login, list file: `ls`  
2. `data.txt` is listed in the home directory
3. Open the file to look at the password
4. Instead of relying on Online decoder tools, I developed a Python Script to handle Caesar Cipher shift programatically.
   - **Source code:** [caesar_cipher.py](https://github.com/ms-Noone/Scripting)
   - **Logic:** The script iterates through the string, identifies the character's ASCII value, and applies the shift while maintaining the case (uppercase/lowercase).   
   - **Usage:** `caesar_cipher.py --shift 13 [--text TEXT] mode`

**Analysis:**
- The vulnerability highlighted here is ROT13 which is simple substitution cipher that provide no real security against attacker.
- Storing passwords in a reversible format without robust access controls or industry-standard encryption leads to an immediate compromise of the system once the file is discovered

## Level 19
**Goal:** Retrieve the password from /etc/bandit_pass/bandit20 by leveraging the provided setuid binary
```
ssh bandit19@bandit.labs.overthewire.org -p 2220
```

**Steps:**  
1. After login, list file:`ls -l`  
   - Confirmed that `bandit20-do` present and has the special permission bit set(suid) :
     <img width="574" height="50" alt="image" src="https://github.com/user-attachments/assets/22b750c8-95b9-405c-80e9-20b10ef48230" />
2. Execute the binary to read the password file:  
   <img width="528" height="40" alt="image" src="https://github.com/user-attachments/assets/c6376347-cc79-4c4f-9c5d-f85af26daeb7" />

**Analysis:**
- The setuid bit allows a program to run with the permission of its owner rather than the user executing it
- Setuid can be dangerous if misconfigured, Attacker often exploit setuid for priviledge escalation, gaining unauthorized access to file or system capabilities
- Best practice is to minimize setuid binaries, audit regularly and ensure they dont allow arbitrary command execution

