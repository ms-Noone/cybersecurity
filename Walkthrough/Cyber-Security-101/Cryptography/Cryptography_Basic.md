# Cryptography – TryHackMe Walkthrough
**Room** : Cryptography Basic  
**Date Completed** : Jan 15, 2026  
**Category** : Cryptography  
**Focus Areas** : Cryptography and symmetric encryption  

## Task 2: Importance of Cryptography

**Concept Learned:**  
  - Cryptography protect confidentiality, integrity, and authenticity
  - PCI DSS requires:  
    a. Minimum security standard for storing, processing, and transmitting cardholder data  
    b. Encryption of data at rest and in motion  

**Security Perspective:**  
  - Confidentiality : avoid using unencrypted protocol during data transmission as this expose plaintext
  - Integrity : use hashes / checksum to verify files or logs haven't been tampered
  - Authenticity : Digital signature & certificates validates the authenticity of communication or files
	
## Task 3: Plaintext to Ciphertext

**Concept Learned:**   
  - Cipher : Algorithm to convert plaintext into a ciphertext or vice versa
  - Encryption : Converting plaintext into ciphertext using a cipher and a key
  - Decryption : Reverse process of encryption

**Security Perspective:**  
  - Data protection : encryption secure data at rest, in transit and in use
  - Confidentiality : ensure only intended recipient can read the data

## Task 4: Historical Ciphers

**Concept Learned:**  
  - Caesar Cipher  
    a. Shift each letter by a certain number to encrypt the message  
		b. Encryption : Shift to right by a chosen number  
		c. Decryption : Shift to left by a same number as encryption   
    <img width="1120" height="480" alt="image" src="https://github.com/user-attachments/assets/77219ff4-8453-428b-9344-f5522cae93c8" />

**Security Perspective:**  
  - Weak security : Caesar cipher is considered insecure because its only have 25 possible keys
  - Brute force risk: An attacker can simply try all possible shifts to expose the plaintext

## Task 5: Type of Encryption

**Concept Learned:**  
  - Symmetric Encryption  
		a. Use same key (private key) to encrypt and decrypt the data  
		b. Fast and efficient for bulk data (e.g., disk encryption, VPN tunnels)  
    
- Asymmetric Encryption  
		a. Use pair of keys:  
		   i. Public Key : Encrypt data  
		   ii. Private Key : Decrypt data  
		d. Commonly used in secure communications (TLS, email, SSH).  

Security Perspective:
	1. The private key must be protected from leaked, if not all data can be decrypted
	2. Symmetric keys must be exchanged through secure communication channel to prevent interception

## Task 6: Basic Math

Concept Learned:
	1. Two mathematical operations used in cryptography:
		a. XOR Operation : Returns 1 if bits are different and 0 if same
		b. Modulo Operation (%) : Remainder when X is divided by Y

Security Perspective:
1. XOR Operation : If keys are weak or reused, attackers can exploit XOR’s predictability to recover plaintext.
2. Modulo Operation : Weak key sizes make systems vulnerable to brute‑force or factorization attacks, reducing encryption strength

## Summary
This rooms builds a fundamental theory of how cryptography is used in modern security practice and highlight its importance in solving the problem we face in digital world
