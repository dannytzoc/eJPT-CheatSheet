## eJPT-Cheatsheet For Exam/Studying


## NMAP
```
nmap -Pn 127.0.0.1
```
-Pn skip host discovery
-sV is used to determine the application version information
-p- scans all port 
-T4 Fast Scan Makes a lot of noise 
-sU udp scan 

## SMB 
```
nmap -p445 --script smb-protocols IPADDRESS #protocols
nmap -p445 --script smb-security-mode IPADDRESS
nmap -p445 --script smb-enum-sessions IPADDRESS

```
