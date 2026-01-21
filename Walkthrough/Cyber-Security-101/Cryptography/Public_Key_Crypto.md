# Public Key Crytography Basic – TryHackMe Walkthrough 
**Room** : Public Key Cryptography Basic  
**Date Completed** : Jan 21, 2026  
**Category** : Cryptography  

**Objective:**  
Understand the fundamentals of asymmetric cryptosystems and their applications, including RSA, Diffie‑Hellman, SSH, SSL/TLS certificates, and PGP/GPG. Demonstrate how these concepts secure communication and how SOC analysts encounter them in practice.

## 📝Task 3: RSA

**Key Takeaways:**  
	• RSA: Asymmetric encryption method used to secure data transmission  
	• Security relies on the difficulty of factoring large number  
	
**Security Perspective:**  
	• Weak key sizes (<2048 bits) are vulnerable to brute force.

## 📝Task 4: Diffie-Hellman

**Key Takeaways:**  
	• Diffie-Hellman: key exchange protocol over an insecure communication channel  
	• Security relies  on the difficulty of solving the discrete logarithm problem in modular arithmetic  

**Security Perspective:**  
Strong parameters are essential; weak ones can be exploited

## 📝Task 5: SSH

**Key Takeaways:**  
	• SSH clients verify server public key fingerprints to prevent MITM attacks  
	• - Authentication uses public/private key pairs (commonly RSA).  
	• Tools: `ssh-keygen` generates key pairs  
	   Commands: `ssh-keygen -t <key_type>`  

**Security Perspective:**  
	• As a user, we must make sure to recognise our server public key as this may lead to MITM attack

## 📝Task 6: Digital Signature and Certificates

**Key Takeaways:**  
	• Digital signature: verify the authenticity and integrity of a digital message  
	• Certificates: rely on a chain of trust to validate source  

**Security Perspective:**  
Chain of trust prevents spoofed or malicious certificates

## 📝Task 7: PGP and GPG

**Key Takeaways:**  
	• PGP : software that implements encryption for files  
	• GPG: widely used in email to protect confidentiality of the email message  
	• Tools: gpg to sign only or sign and encrypting  
	  Commands: `gpg --full-generate-key`  

**Security Perspective:**  
Protects against email tampering and ensures confidentiality

## Summary

This room reinforced the importance of asymmetric cryptography in securing communications. For a SOC analyst, recognizing weak implementations (e.g., small RSA keys, untrusted certificates, or fingerprint mismatches) is critical for detecting vulnerabilities and preventing attacks
