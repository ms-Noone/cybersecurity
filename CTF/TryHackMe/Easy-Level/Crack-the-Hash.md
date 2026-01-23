# TryHackMe : Crack the Hash
This walkthrough documents my solutions for the TryHackMe Crack the Hash Challenge. To solve this challenge, we can choose several tools to identify and crack the hashes. 
Lets start the challenge!

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

## Result

       




