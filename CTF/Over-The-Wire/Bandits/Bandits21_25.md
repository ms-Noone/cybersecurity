# OverTheWire: Bandit Level 21-25
This walkthrough documents my solutions for the OverTheWire Bandit wargame. Bandit is designed to teach Linux basics, command-line usage, and security concepts.  

## 🔑 Level 21 → Level 22
**Goal:** Retrieving the password for the next level (bandit22) from a program that is automatically executed by cron

```
ssh bandit21@bandit.labs.overthewire.org -p 2220
# password: EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

**Steps:**  
1. Login using SSH command above
2. Check what command being executed by cron: `cat /etc/cron.d/cronjob_bandit22`
   <img width="519" height="51" alt="image" src="https://github.com/user-attachments/assets/8f578a81-e28b-4761-8cd6-8b13070241cb" />
3. Inspect the script content of script been run by cronjob: `cat /usr/bin/cronjob_bandit22.sh`
   <img width="603" height="70" alt="image" src="https://github.com/user-attachments/assets/6c690d10-9e5b-4d9c-ac2a-3d5b8dc36cac" />
4. Retrieve password from the output file mention in step 3: `cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`
   <img width="573" height="35" alt="image" src="https://github.com/user-attachments/assets/de320415-e04a-4cd5-8098-464456d495c6" />

**Analysis:**  
This exercise demonstrates how a lower‑privileged user can access secrets when a cronjob writes sensitive data into a file with overly permissive access rights

**Password for Level 22c:**  
`tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q`#Passwords shown are from OverTheWire Bandit and reset periodically

## 🔑 Level 21 → Level 22
**Goal:** 

**Steps:**

