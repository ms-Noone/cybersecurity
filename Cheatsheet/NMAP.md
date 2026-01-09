# 🛠️ NMAP – Command Cheat Sheet  
This cheat sheet was created to capture useful commands for quick future reference

## Scanning Types
| Syntax | Example Command  | Description |
| ------------- | ------------- | ------------- |
| -sT | `nmap -sT IP` | TCP Connect scan by complete full handshake |
| -sS | `nmap -sS IP` | TCP Syn scan |
| -sU | `nmap -sU IP` | UDP scan |
| -PR | `nmap -PR -sn IP` | Indicate to scan only with ARP request |  
| -v | `nmap IP -v` | Real-time Scan Progress |


## Host Discovery
| Syntax | Example Command  | Description |
| ------------- | ------------- | ------------- |
| -sn | `nmap -sn IP` | Discover live host without probing services |
| -sL | `nmap -sL IP` | Enumerate live host without scanning |

## Port Option
| Syntax | Example Command  | Description |
| ------------- | ------------- | ------------- |
| -p- | `nmap -p- IP` | Scans all ports |
| -p <PortNo> | `nmap -p PortNo IP` | Scans specific port|

## Version Detection
| Syntax | Example Command  | Description |
| ------------- | ------------- | ------------- |
| -sV| `nmap -sV IP` | Service and Version detection |
| -O | `nmap -O IP` | OS fingerprinting |
| -A | `nmap -A IP` | OS detection, version detection, and other additions | 
