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
