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

## Transfering Files
 






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












