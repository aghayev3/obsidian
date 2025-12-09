## DHCP Snooping 
- DHCP snooping is a security feature used in network switches to prevent unauthorized devices from acting as DHCP servers and distributing incorrect IP address information. It works by monitoring DHCP messages, classifying switch ports as trusted or untrusted, and blocking any suspicious DHCP traffic from untrusted sources. Example config from an HP Switch:
```
dhcp-snooping
dhcp-snooping authorized-server 10.0.110.10
dhcp-snooping authorized-server 10.0.110.89
dhcp-snooping database file "tftp://10.200.100.100/10.200.17.12"
no dhcp-snooping option 82
dhcp-snooping vlan 10-11 16 19-21 30-31 50 52 65 90 110 510
interface 47
   dhcp-snooping trust
interface 48
   dhcp-snooping trust
```
- This enables DHCP snooping, tells the switch which servers are authorized, saves the binding table via TFTP, disables Option 82, and enables DHCP Snooping on certain VLANs. Ports 47-48 are uplinks and trusted. 
- DHCP Snooping Binding is a database that records the association between IP addresses and MAC addresses of devices that have successfully completed a DHCP transaction on a network. This binding helps to prevent unauthorized devices from acting as DHCP servers and enhances overall network security.
- For example: 
```
RH-GRB-3D2# show dhcp-snooping binding


  MacAddress    IP              VLAN Interface Time Left
  ------------- --------------- ---- --------- ---------
  10604b-72a9c1 10.11.0.163     11   4         34453
  704d7b-6f24cf 10.11.0.202     11   1         35263
  a08cfd-e0e8ab 10.11.1.118     11   30        22016
  ac162d-0e077d 10.11.0.191     11   23        37479
  b4b52f-d2f492 10.11.0.183     11   18        33389
  d02788-dc1aba 10.11.0.236     11   29        36455
  e83935-3bccfc 10.11.0.140     11   31        29880
  e83935-3dc532 10.11.0.124     11   19        42586
  881544-a9eeae 10.21.21.119    21   27        581988
  2401c7-827ec1 10.30.1.218     30   42        22016
  54781a-1cc27a 10.30.1.42      30   19        22043
  54781a-1cc399 10.30.1.81      30   31        22045
  54781a-1cc3df 10.30.1.179     30   18        22053
  54781a-1cc9af 10.30.1.214     30   26        23686
  54781a-1cca08 10.30.1.94      30   30        22056
  54781a-1cca72 10.30.1.183     30   12        24303
  54781a-1ccc27 10.30.1.60      30   33        22102
  54781a-1cf6dc 10.30.1.46      30   42        22018
  54781a-1d443c 10.30.1.192     30   32        22049
  58bfea-204d16 10.30.1.216     30   4         22041
  a41875-8bc6bf 10.30.1.70      30   23        22058
```

## Instrumentation Monitor
- The operational thresholds that are monitored on the switch. By default, the instrumentation monitor is disabled. Syntax:
```
instrumentation monitor [parameterName|all] [<low|med|high|limitValue>] 
no instrumentation monitor [parameterName|all] [<low|med|high|limitValue>]
```
- Its purpose is to detect loops, scanning, anomalies, MAC floods, login failures, etc. and providing logs/alerts.

## Logging

```
logging 10.200.100.102
logging severity warning
```
- Syslog server at 10.200.100.102
- A syslog server is a centralized logging system that collects, stores, and organizes log messages from various network devices, servers, and applications.
- The switch only sends Warnings or higher
- Other available options are `debug, info, warning, error, major`

## Port Security 
- Port Security typically involves configuring switches to allow only specific MAC addresses or limiting the number of devices that can connect to a port, enhancing overall network security. Example on HP Switch: 
```
port-security 1 learn-mode limited-continuous
port-security 1 address-limit 32
port-security 1 action send-alarm
no port-security 1 eavesdrop-prevention
```
- In this case the port dynamically learns up to 32 MAC addresses and if that number is exceeded it sends and alarm but doesn't stop learning and allowing new MACs. In this case the limit is purely a monitoring threshold. 
- Port Security prevents the following
	- MAC flooding attacks
	- Unauthorized devices being plugged in
	- ARP spoofing (via eavesdrop prevention)
- It shouldn't be applied on uplink ports because that would cause chaos because of so many MACs
- Eavesdrop prevention blocks ARP poisoning, but might cause compatibility issues with some devices

## sFlow
- Short for "sampled flow" is a traffic monitoring protocol
- It samples packets and interface statistics on a switch and sends them to a collector for analysis.
```
sflow 1 destination 10.200.100.102
sflow 1 polling 36 30
sflow 1 sampling 36 200
```
- The collector is 10.200.100.102, the switch reports statistics for port 36 every 30 seconds and samples one out of every 200 packets on that port