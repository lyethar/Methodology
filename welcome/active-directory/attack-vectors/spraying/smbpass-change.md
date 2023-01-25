# SMBPass Change

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
