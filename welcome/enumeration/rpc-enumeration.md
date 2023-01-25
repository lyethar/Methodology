# RPC Enumeration



```
rpcclient -U "" 192.168.105.122

if anonymous is allowed wihout passwordd
type 
enumdomusers
enumprinters

To make a list out of these users to spray passwords and aeseproast

rpcclient -U "" <ip> -N -c "enumdomusers" | grep -oP '\[.*?\]' | grep "0x" -v | tr -d '[]' > userlist.txt
```

Authenticated&#x20;

RPCEnumaAuthenticated binary that i got from savitar we just have change the -U "USERNAME%PASSWORD" and take out the -N&#x20;
