# Pivoting

{% embed url="https://oscp.infosecsanyam.in/pivoting" %}

{% embed url="https://sushant747.gitbooks.io/total-oscp-guide/content/port_forwarding_and_tunneling.html" %}

{% embed url="https://0xdf.gitlab.io/2020/08/10/tunneling-with-chisel-and-ssf-update.html" %}

### Discovering New Targets&#x20;

The trick here is to look for more IP addresses that are hidden. Look for ones that we didn't get from the initial ping sweep.

#### Meterpreter session

Look for more interfaces

```
ifconfig 
arp
route

```

#### Shell

Look at ALL the output.

```
ipconfig /all 
ipconfig /displaydns
netstat -ano
```

#### Ping Sweep

```
use post/multi/gather/ping_sweep
set the RHOSTS 101010/24
```

#### ARP Scanner&#x20;

Meterpreter

```
run arp_scanner -r 10.10.10.0/24
```

### Routing&#x20;

```
meterpreter > run autoroute -s 172.30.111.0/24
use autoroute module 
```

### Port Scan

```
Run tcp portscan change threads to 10, and change ports to smaller.
```

### Proxying

```
search socks server
use
set port
edit /etc/proxychains4.conf
edit the last line to
socks4 127.0.0.1 1080
or socks5 
```

Start by saying proxychain and then the command

we can also use proxychains to start our web browser.

### Port Forwarding with Metasploit

Lets say we want to access a web server on port 80 on the victim machine.

```
portfwd add -l 8080 -p 80 <ip of victim that has the web server> 
```
