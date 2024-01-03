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




