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

```


















