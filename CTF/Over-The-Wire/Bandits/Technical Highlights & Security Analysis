# OverTheWire: Bandit — Technical Highlights & Security Analysis
While completing the Bandit series, i selected few level that highlight and demonstrated my proficiency in Linux system administration, vulnerability analysis and custom tool development

## 🔑 Level 11 → Level 12
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
