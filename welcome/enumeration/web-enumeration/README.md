# Web Enumeration

### CheatSHEET

{% embed url="https://strongcourage.github.io/2020/05/03/enum.html" %}

{% embed url="https://fareedfauzi.gitbook.io/oscp-notes/services-enumeration/http-s/enumeration-checklist" %}

{% embed url="https://book.hacktricks.xyz/network-services-pentesting/pentesting-web" %}

Use exiftool on pngs and documents that might give you a hint on the owner.&#x20;

### Directory Busting&#x20;

#### IIS Applications

```
wfuzz -c --hc=404 -t 200 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/IIS.fuzz.txt http://10.10.10.103:80/FUZZ
```
