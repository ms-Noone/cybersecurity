# 🛠️ NMAP – Command Cheat Sheet  
This cheat sheet was created to capture useful commands for quick future reference

| Feature | Syntax | Example Command  | Description |
| ------------- | ------------- | ------------- | ------------- |
| Host Discovery | -sn | `nmap -sn IP` | Discover live host without probing services |
| Host Discovery | -sL | `nmap -sL IP` | List live host without scanning |
| Port Scanning | -sT | `nmap -sT IP` | TCP Connect scan by complete full handshake |
| Port Scanning | -sS | `nmap -sS IP` | TCP Syn scan |
| Port Scanning | -sU | `nmap -sU IP` | UDP scan |
| Port Scanning | -p- | `nmap -p- IP` | Scans all ports |
| Version Detection | -sV| `nmap -sV IP` | Service and Version detection |
| OS Fingerprinting | -O | `nmap -O IP` | OS fingerprinting |
| Version & OS detction | -A | `nmap -A IP` | OS detection, version detection, and other additions | 
| Verbosity | -v | `nmap IP -v` | Real-time Scan Progress |
| ARP Request | -PR | `nmap -PR -sn IP` | Indicate to scan only with ARP request |  

