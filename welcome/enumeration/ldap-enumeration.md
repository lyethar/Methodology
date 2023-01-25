# LDAP Enumeration

EXAMINE EVERYTHING FABIAN, LOOK AT WEIRD Fields that have been added for users. !!!

Try to grep the following just in case but if it doesnt work look through the output!

```
nmap -n -sV --script "ldap* and not brute" -p389,3268 192.168.105.122

Null bind

ldapsearch -x -H 'ldap://192.168.105.122:389' -D '' -w '' -b "DC=hutch,DC=offsec"
rerun the same command and run it with 
 | grep description sometimes they have interesting things. 
 
 
 ldapsearch -x -H 'ldap://10.10.10.182:389' -D '' -w '' -b "DC=cascade,DC=local" | grep Pwd
 ldapsearch -x -H 'ldap://10.10.10.182:389' -D '' -w '' -b "DC=cascade,DC=local" | grep pwd
 ldapsearch -x -H 'ldap://10.10.10.182:389' -D '' -w '' -b "DC=cascade,DC=local" | grep password
 ldapsearch -x -H 'ldap://10.10.10.182:389' -D '' -w '' -b "DC=cascade,DC=local" | grep Pass
 ldapsearch -x -H 'ldap://10.10.10.182:389' -D '' -w '' -b "DC=cascade,DC=local" | grep pass
```

This command is to make a list of existing users.&#x20;

```
ldapsearch -x -H 'ldap://10.10.10.172:389' -D '' -w '' -b "DC=MEGABANK,DC=LOCAL" | grep sAMAccountName | tr -d ':' | sed 's/s//' | sed 's/A//' | sed 's/M//' | sed 's/A//'| sed 's/c//' | sed 's/c//'| sed 's/o//' | sed 's/u//' | sed 's/n//'| sed 's/t//' | sed 's/N//'| sed 's/a//' | sed 's/m//' | sed 's/e//' > ldapusers.txt
```

#### Authenticated&#x20;

```
ldapsearch -H ldap://10.10.10.248 -x -W -D "Ted.Graves@intelligence.htb" -b "dc=intelligence,dc=htb"
```

We could make a new directory and use this command and host a python webserver.

```
ldapdomaindump -u 'htb.local\amanda' -p 'Ashare1972' 10.10.10.103
[*] Connecting to host...
[*] Binding to host
[+] Bind OK
[*] Starting domain dump
[+] Domain dump finished

```

If a group is part of the Remote management Group, it means we can log in via winrm.
