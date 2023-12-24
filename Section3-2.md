## Network based Attacks 
Packets traveling across the network 
+ ArP DHCP FTP Telnet SSH
+ Man in the Middle Traffic Might hit all points hubs are things in the past
+ ARP posiing start broadcasting ARP and say you are the certin address
+ SPoof with ARP posining

## Wireshark 
+ Frake is going to cover attention 
+ Then destination 
+ then its the packet 
+ Follow HTTP Stream
+ Display Feature Expression - filter anym sort of network traffic
+ export http


## TSHARK
```
tshark -h
tshark -v
tshark -D #list interface
tshark -i # pick interface
tshark -r pcap_file
tshark -r pcap_file -z io,phs -q #hireacrhy

tshark -r pcacp_file -Y "http"
tshark -r pcacp_file -Y "ip.src==ip && ip.dest==ip"
tshark -r pcacp_file -Y "http.request.method==GET" -Tfields -e frame.time -e ip.src -e http.request.full_uri
tshark -r pcacp_file -Y "http contains password"

```
## ARP Posining 
```
echo 1 > /proc/sys/net/ipv4/ip_forward
arpspoof -i eth1 -t client_ip -r server_ip #traffic to tell that we are 36 to 37

```
## Wif Traffic Analysis 
```
tshark
tshark -r pcapfile -Y 'wlan'
tshark -r pcapfile -Y 'wlan.fc.type_subtype==0x00c'
tshark -r WiFi_traffic.pcap -Y "eapol"

tshark -r pcapfile -Y 'wlan.fc.type_subtype==8' -Tfields -e wlan.ssid -e wlan.bssid
tshark -r pcapfile -Y 'wlan.ssid==LazyArtists' -Tfields -e -e wlan.bssid

tshark -r pcapfile -Y 'wlan.ssid==Home_Nework' -Tfields -e -e wlan.radio.channel
tshark -r pcapfile -Y "wlan.fc.type_subtype==0x000c" -Tfields -e wlan.ra
tshark -r pcapfile -Y 'wlan.ta==MAC && http' -Tfields -e http.user_agent





```




