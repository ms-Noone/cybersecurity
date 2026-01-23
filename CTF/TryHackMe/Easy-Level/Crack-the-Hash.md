# TryHackMe : Crack the Hash
This walkthrough documents my solutions for the TryHackMe Crack the Hash Challenge. The goal is to identify different hash type and crack them using online tools or GPU-powered software like Hashcat.

**Tools & Resource:**
1. [CrackStation](https://crackstation.net/) - Online password hashed cracker
2. Hashcat - Open source software to crack the hash, installed on your local machine since this require the GPU capability to crack the password
3. [HashID](https://hashes.com/en/tools/hash_identifier) - Hash type identifier
4. [Hash Mode](https://hashcat.net/wiki/doku.php?id=hashcat) - Hash mode identifier

## Steps
1. Use HashID to determine the algorithm
   ex:  
   <img width="1597" height="528" alt="image" src="https://github.com/user-attachments/assets/0a68f300-b95c-4c98-997f-ac8ea1dd7703" />
2. Crack the hash
   - Option A: Crackstation
     - Paste the hashes into CrackStation
     - If it's a common password, Crackstation will return the plaintext immediately
       ex:
       <img width="1095" height="464" alt="image" src="https://github.com/user-attachments/assets/bfa4fa79-e921-4f0b-994d-367b6ceca455" />

    - Option B: Hashcat
      - Run hashcat with identified hash type and correct mode
      - Example command: `hashcat -m 100 -a 0 hash.txt rockyou.txt`
        - `-m 100` → SHA1 mode
        - `-a 0` → Dictionary attack
        - `hash.txt` → File containing the hash
        - `rockyou.txt` → Wordlist


## Result
| Hashes  | Hashes ID | Mode | Output | 
| ------------- | ------------- | ------------- | ------------- |
| 48bb6e862e54f2a795ffc4e541caed4d | md5 | 0 | _easy_ |
| CBFDAC6008F9CAB4083784CBD1874F76618D2A97  | SHA1 | 100 | _password123_ |
| 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032 | SHA256 | 1400 | _letmein_ |
| $2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom | bcrypt | 3200 | |
| 279412f945939ba78ce0758d3fd83daa | md4 | 900 | _Eternity22_ |
| F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85 | SHA256 | 1400 | _paule_ |
| 1DFECA0C002AE40B8619ECF94819CC1B | NTLM | 1000 | _n63umy8lkf4i_ |
| $6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02. | sha512crypt | 1800 | |
| e5d8870e5bdd26602cab8dbe07a942c8669e56d6 | md5 | 0 | |

## Conclusion
   - Weak hashes like MD5 and SHA1 can be cracked instantly, we can even use online tool to crack the hash
   - Stronger hashes will show as unknown when tried to crack by online tool, therefore it require GPU capability and time-intensive cracking to crack the password.
   - This challenge emphasize the importance of having stronger hashes and defensive measure like salting , peppering and rate-limiting

       




