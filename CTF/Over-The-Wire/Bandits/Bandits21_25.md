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

**Password for Level 22:**  
`tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q`#Passwords shown are from OverTheWire Bandit and reset periodically

## 🔑 Level 22 → Level 23
**Goal:** Retrieving the password for the next level (bandit23) from a program that is automatically executed by cron

**Steps:**
1. Login using SSH command: `ssh bandit22@bandit.labs.overthewire.org -p 2220`
2. Check what command being executed by cron: `cat /etc/cron.d/cronjob_bandit23`
3. Inspect the script content of script been run by cronjob: `cat /usr/bin/cronjob_bandit23.sh`
   <img width="639" height="146" alt="image" src="https://github.com/user-attachments/assets/8581c11c-34b0-4e74-8bd4-8a98aa209d52" />
4. Run the command from step 3 output manually to get the password filename:
   <img width="662" height="31" alt="image" src="https://github.com/user-attachments/assets/49f693ba-bd79-4513-95aa-fd5626a3e316" />
5. Retrieve password from the output file mention in step 4: `cat /tmp/8ca319486bfbbc3663ea0fbe81326349`
   <img width="642" height="33" alt="image" src="https://github.com/user-attachments/assets/a76f260e-3f4e-429f-bc21-23107796f474" />

**Password for Level 23:**  
`0Zf11ioIjMVN551jX3CmStKLYqjk54Ga`#Passwords shown are from OverTheWire Bandit and reset periodically

## 🔑 Level 23 → Level 24
