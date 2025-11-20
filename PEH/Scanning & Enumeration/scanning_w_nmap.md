# Scanning with nmap

![[Pasted image 20251120152032.png]]

---
## find kioptrix's IP
- use `arp-scan -l` to find the IPs of the devices on the local network
- or log in to kioptrix and `ping 8.8.8.8`, the ping command shows the local IP
- or `netdiscover -r <network>`
## nmap
```
nmap -T4 -p- -A <target-IP>
```