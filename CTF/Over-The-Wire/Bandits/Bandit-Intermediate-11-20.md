# OverTheWire: Bandit Level 11-15
This walkthrough documents my solutions for the OverTheWire Bandit wargame. Bandit is designed to teach Linux basics, command-line usage, and security concepts.  

## 🔑 Level 11 → Level 12
**Goal:** Retrieve the password stored in `data.txt` where the password is encoded with ROT13
```
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

**Steps:**  
1. After login, list file: `ls`  
2. `data.txt` is listed in the home directory
3. Open the file to look at the password
4. To decode it, i did use my own script rather than relying on existing or online tools. I keep the script in my repo [here](https://github.com/ms-Noone/Scripting)
   - usage: `caesar_ciper.py [--shift SHIFT] [--text TEXT] mode`
   - ran the script with shift 13, and it will cleanly revealed the password for next level


