# SMB Enumeration

### Version Check

```
use auxiliary/scanner/smb/smb_version
```

### List

```
smbclient --no-pass -L //<IP> # Null user
smbclient -U 'username[%passwd]' -L [--pw-nt-hash] //<IP> #If you omit the pwd, it will be prompted. With --pw-nt-hash, the pwd provided is the NT hash
smbmap -H <IP> [-P <PORT>] #Null user
smbmap -u "username" -p "password" -H <IP> [-P <PORT>] #Creds
smbmap -u "username" -p "<NT>:<LM>" -H <IP> [-P <PORT>] #Pass-the-Hash
crackmapexec smb <IP> -u '' -p '' --shares #Null user
crackmapexec smb <IP> -u 'username' -p 'password' --shares #Guest user
crackmapexec smb <IP> -u 'username' -H '<HASH>' --shares #Guest user
```

### Connect&#x20;

```
#Connect using smbclient
smbclient --no-pass //<IP>/<Folder>
smbclient -U 'username[%passwd]' -L [--pw-nt-hash] //<IP> #If you omit the pwd, it will be prompted. With --pw-nt-hash, the pwd provided is the NT hash
#Use --no-pass -c 'recurse;ls'  to list recursively with smbclient

#List with smbmap, without folder it list everything
smbmap [-u "username" -p "password"] -R [Folder] -H <IP> [-P <PORT>] # Recursive list
smbmap [-u "username" -p "password"] -r [Folder] -H <IP> [-P <PORT>] # Non-Recursive list
smbmap -u "username" -p "<NT>:<LM>" [-r/-R] [Folder] -H <IP> [-P <PORT>] #Pass-the-Hash
```

### Mount them to see if we have write access to them

```
mount -t cifs //10.10.10.103/'Department Shares'/ /home/kali/Sizzle/results/mount
```

By using the command tree we can easily list the files inside the directory although we would already know this with autrecon.![](../../../.gitbook/assets/2022-08-11\_13-03.png)

So in order to enumerate permissions within these folders to see which we would have access to write and maybe we can put some sort of malicious files such as .hta, .scf, or any other based on the software that the company might seem to have.&#x20;

```
tput civis; for directory in $(ls); do echo -e "\n [*] Enumerating Permissions in the $directory:\n"; echo -e "\t$(smbcacls "//10.10.10.103/Department Shares" Users/$directory -N | grep "Everyone")"; done; tput cnorm
```

![](../../../.gitbook/assets/2022-08-11\_13-12.png)

So edit accordingy, the script basically says that within the items in the command ls, we will run the smbcacls command. To see who has write permissions.&#x20;

### Brute Force&#x20;

```
nmap --script smb-brute -p 445 <IP>
hydra -L /usr/share/seclists/Usernames/top-usernames-shortlist.txt -P /usr/share/seclists/Passwords/Common-Credentials/best15.txt 10.130.40.70 smb -t 1
crackmapexec smb 10.129.155.73 -u /usr/share/seclists/Usernames/top-usernames-shortlist.txt -p /usr/share/seclists/Passwords/darkweb2017-top100.txt
```

```
nmap --script smb-brute -p 445 <IP>
ridenum.py <IP> 500 50000 /root/passwds.txt #Get usernames bruteforcing that rids and then try to bruteforce each user name
```
