## Intro To Web 
+ HTML,CSS,Javascript 
+ Fetch files using web servers or using other services such as Word PRess Azure 

### Requests 
+ Methods to retrieve data 
+ GET,Head,Post,Put,Delete,Connect,Options, Trace, Push 
+ Get back are response such as 200,302,404
+ Session are code along side request for tracking login 

### HTTPS
+ TLS,SSl encrypted data over the internet

## dirb Commnad
```
dirb url 
```
## curl commands 
```
curl -X COMMAND IP_OR_URL -v
curl -I IP_OR_URL
curl -XPUT IP_OR_URL
curl IP_URL --upload-file hello.txt  # if put allowed
curl -XDELETE IP_OR_URL
```

## gobuster 
```
gobuster dir -u URL -w /usr/share/wordlists/dirb/common.txt
gobuster dir -u URL -w /usr/share/wordlists/dirb/common.txt -b 403,404
gobuster dir -u URL -w /usr/share/wordlists/dirb/common.txt -b 403,404 -x .php,.xml,.txt -r


```

## Nikto 
```
nikto -h url

nikto -h ur; -Tuning 5 -Display V 

nikto -h ur; -Tuning 5 -Display V  -o outputformat -F format


```
## Burp Suite Directory Enumeration
```
send to intruder
clear
add name to GET
set to sniper
then go to payload
load wordlist

```
## Burp Suite Crawling

```
click on live crawling from Proxy on Dashboard
```

## SQLMAP
```
GET
sqlmap -u "URL" --cookie "cookie_value" -p which_var_to_target

sqlmap -u "URL" --cookie "cookie_value" -p which_var_to_target --dbs #drops database

sqlmap -u "URL" --cookie "cookie_value" -p which_var_to_target -D database_name --tables #drops tables


sqlmap -u "URL" --cookie "cookie_value" -p which_var_to_target -D database_name -T table_name --columns #drops columns

sqlmap -u "URL" --cookie "cookie_value" -p which_var_to_target -D database_name -T table_name -C columnname,columnname --dump #drops all the info from columns

POST
copy request to file

sqlmap -r file -p request_variable

```

## Xsser 
```
xsser --url url -p payload #in payload include XSS on payload field
xsser --url url -p payload --auto
xsser --url url -p payload --Fp custom_payload #in payload include XSS on payload field
 xsser --url “URL” --cookie=”COOKIE” --Fp “<script>alert(1)</script>”
```

## Hydra Login 
```
hydra -L users.txt -P passwords.txt IP_URL http-post-form "/file.php:PARAMETERS:Invalid Creds!" 
```

## Burp Suite Basic Auth 
```
caputre login request
send it to intruder
clear
high kight login info
load password
add prefix o suffix
encode base64
start attack 
```
ZAP HTTP Login Form
```
right click
fuzz highlight text
add list

```








