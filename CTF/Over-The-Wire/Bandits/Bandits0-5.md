# OverTheWire: Bandit Level 0-5
This walkthrough documents my solutions for the OverTheWire Bandit wargame. Bandit is designed to teach Linux basics, command-line usage, and security concepts.  

## 🔑 Level 0 → Level 1
**Goal:** Retrieve the password for the next level.  
**Connection:**  
```
ssh bandit0@bandit.labs.overthewire.org -p 2220
# password: bandit0
```
**Steps:**  
1. After login, verify current directory: `pwd`
2. If confirm in /home/bandit0, list files: `ls`
3. Else, change directory to home: `cd ~` then list files `ls`
4. `readme` file is listed in the home directory
5. Display contents: `cat readme`
6. Output:  
   <img width="722" height="134" alt="image" src="https://github.com/user-attachments/assets/ae6b8b1c-55a8-4c9a-aa65-003cf45afb6c" />

**Analysis:**  
- Password stored in basic simple text file
- This challenge highlights the importance of confirming directory context before accessing files

**Password for Level 1:**  
`_ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If_`  _#Passwords shown are from OverTheWire Bandit and reset periodically_

## 🔑 Level 1 → Level 2
**Goal:** Password stored in a file called `-`  
**Steps:**  
1. After login, verify current directory: `pwd`
2. If confirm in /home/bandit0, list files: `ls`
3. Else, change directory to home: `cd ~` then list files `ls`
4. `-` file is listed in home directory
5. Display contents: `cat ./-`
6. Output:  
   <img width="644" height="61" alt="image" src="https://github.com/user-attachments/assets/eaf2b820-0f6a-45f5-a56a-c3f6587e705c" />

**Analysis:**  
- Dashed filename caused command-line confusion and will also break the automation script if not handled properly
- This challenge show that edge case must be handled properly as it can cause unexpected issue

**Password for Level 2:**  
`263JGJPfgU6LtdEvgfWU1XP5yac29mFx`  _#Passwords shown are from OverTheWire Bandit and reset periodically_

## 🔑 Level 2 → Level 3
**Goal:** Password stored in a file name `--spaces in this filename--`  
**Steps:**  
1. After login, verify current directory: `pwd`
2. If confirm in /home/bandit0, list files: `ls`
3. Else, change directory to home: `cd ~` then list files `ls`
4. `--spaces in this filename--` file is listed in home directory
5. Display contents: `cat ./"--spaces in this filename--"`
6. Output:  
   <img width="698" height="87" alt="image" src="https://github.com/user-attachments/assets/478ee589-9b68-4581-b655-3607d8665600" />

**Analysis:**  
- Spaces in filename cause command execution and automation script to break, they also lead to broken filepath in Web/URL
- Users, developers or analyst should avoid special character in filename as command may interpret them as multiple separate arguments

**Password for Level 3:**  
`MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`  _#Passwords shown are from OverTheWire Bandit and reset periodically_

## 🔑 Level 3 → Level 4
**Goal:** Password stored in a hidden file in `inhere` directory  
**Steps:**  
1. After login, change directory: `cd inherent`
2. List hidden files: `ls -a`
3. `...Hiding-From-You` file is listed
4. Display contents: `cat ...Hiding-From-You`
5. Output:  
   <img width="747" height="92" alt="image" src="https://github.com/user-attachments/assets/2a60a658-b21b-493d-be88-00883c1f1f81" />

 

**Analysis:**  
- 

**Password for Level 4:**  
`2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`  _#Passwords shown are from OverTheWire Bandit and reset periodically_
