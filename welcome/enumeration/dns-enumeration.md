# DNS Enumeration

{% embed url="https://pentestlab.blog/tag/reverse-lookup/" %}

{% embed url="https://github.com/darkoperator/dnsrecon" %}

Enumerating Domain Name System or DNS can help reveal a larger scope for potential attacks.&#x20;

&#x20;

```
dig cyberbotic.io +short

follow up with: 
whois <dns.io>

nslookup

SERVER victim-ip

127.0.0.1

victim-ip again
```

![](<../../.gitbook/assets/image (42).png>)

```
dig axfr cronos.htb @10.10.10.13
```

![](<../../.gitbook/assets/image (27).png>)

We then add those subdomains to our /etc/hosts file.



### Little Cheatsheet

| **Command**                        | **Description**                                      |
| ---------------------------------- | ---------------------------------------------------- |
| `nslookup $TARGET`                 | Identify the `A` record for the target domain.       |
| `nslookup -query=A $TARGET`        | Identify the `A` record for the target domain.       |
| `dig $TARGET @<nameserver/IP>`     | Identify the `A` record for the target domain.       |
| `dig a $TARGET @<nameserver/IP>`   | Identify the `A` record for the target domain.       |
| `nslookup -query=PTR <IP>`         | Identify the `PTR` record for the target IP address. |
| `dig -x <IP> @<nameserver/IP>`     | Identify the `PTR` record for the target IP address. |
| `nslookup -query=ANY $TARGET`      | Identify `ANY` records for the target domain.        |
| `dig any $TARGET @<nameserver/IP>` | Identify `ANY` records for the target domain.        |
| `nslookup -query=TXT $TARGET`      | Identify the `TXT` records for the target domain.    |
| `dig txt $TARGET @<nameserver/IP>` | Identify the `TXT` records for the target domain.    |
| `nslookup -query=MX $TARGET`       | Identify the `MX` records for the target domain.     |
| `dig mx $TARGET @<nameserver/IP>`  | Identify the `MX` records for the target domain.     |

### Subdomain Enumeration&#x20;

{% embed url="https://github.com/rbsec/dnscan" %}

[https://nuclei.projectdiscovery.io/nuclei/get-started/](https://nuclei.projectdiscovery.io/nuclei/get-started/)

### Spoofcheck

Weak email security (SPF, DMARC and DKIM) may allow us to spoof emails to appear as though they’re coming from their own domain. [Spoofcheck](https://github.com/BishopFox/spoofcheck) is a Python tool that can verify the email security of a given domain.

```
$ ./spoofcheck.py cyberbotic.io
[+] cyberbotic.io has no SPF record!
[*] No DMARC record found. Looking for organizational record
[+] No organizational DMARC record
[+] Spoofing possible for cyberbotic.io!
```
