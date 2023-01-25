# Methodology

### Enumerate DNS information

[https://app.gitbook.com/s/yTPWZkKJbJfX8uHiRzmn/\~/changes/RE8l5bVLgRbh4r2fHiJY/welcome/enumeration/dns-enumeration](../dns-enumeration.md)

Zone transfer

{% embed url="https://book.hacktricks.xyz/network-services-pentesting/pentesting-dns#zone-transfer" %}

Retrieve records for every subdomain that is found.&#x20;

using the dig command we can achieve this focus as well on the ones that are 127.0.0.1

reuse the commands for every single one of them.

### Enumerate Subdomains&#x20;

dnscan.py&#x20;

theharvester

```bash
dnsrecon -a -d tesla.com
```

### Enumerating Firewalls

```shell-session
wafw00f -v https://www.tesla.com
```

### Enumerating Technologies&#x20;

#### WhatWeb

```shell-session
whatweb -a3 https://www.facebook.com -v
```

#### Aquatone

**Installing Aquatone**

```shell-session
lyethar-1@htb[/htb]$ sudo apt install golang chromium-driver
lyethar-1@htb[/htb]$ go get github.com/michenriksen/aquatone
lyethar-1@htb[/htb]$ export PATH="$PATH":"$HOME/go/bin"
```

#### Nuclei&#x20;

{% embed url="https://nuclei.projectdiscovery.io/nuclei/get-started/" %}
