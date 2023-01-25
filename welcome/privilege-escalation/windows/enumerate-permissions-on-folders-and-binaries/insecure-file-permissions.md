# Insecure File Permissions

Insecure File permissions happen whenever a low privilege user has the right to overwrite a binary with a payload of their own. Upon restarting of the service, whether that is through manual shutdown of the computer or manual restart of the service, upon the restart, the attacker will receive an administrative shell.&#x20;

* [ ] Restart Service?
* [ ] Can we shut down the system?
* [ ] Can we write the Program?

### Enumeration:

```
## Insecure Folder Permission
C:\>cacls C:\bd
C:\bd BUILTIN\Administrators:(OI)(CI)(ID)F
      NT AUTHORITY\SYSTEM:(OI)(CI)(ID)F
      BUILTIN\Users:(OI)(CI)(ID)R
      NT AUTHORITY\Authenticated Users:(ID)C
      NT AUTHORITY\Authenticated Users:(OI)(CI)(IO)(ID)C

## Insecure File/Service Permission
C:\>cacls C:\bd\bd.exe
C:\bd\bd.exe BUILTIN\Administrators:(ID)F
             NT AUTHORITY\SYSTEM:(ID)F
             BUILTIN\Users:(ID)R
             NT AUTHORITY\Authenticated Users:(ID)C

C:\>sc qc bd
[SC] QueryServiceConfig SUCCESS

SERVICE_NAME: bd
        TYPE               : 10  WIN32_OWN_PROCESS
        START_TYPE         : 2   AUTO_START
        ERROR_CONTROL      : 1   NORMAL
        BINARY_PATH_NAME   : "C:\bd\bd.exe"
        LOAD_ORDER_GROUP   :
        TAG                : 0
        DISPLAY_NAME       : BarracudaDrive ( bd ) service
        DEPENDENCIES       : Tcpip
        SERVICE_START_NAME : LocalSystem

```

Based on the icacls output we see that Users have the permission to write the binary, this can usually be detected by winPEAS and other scripts.

We overwrite the binary with a reverse shell and we restart the service or the machine and we get a reverse shell as Administrator.&#x20;

<details>

<summary>Examples of exploitation of IFP</summary>

[https://app.gitbook.com/s/FBsiDeuhN5SJcOCFJbtD/priv-esc](https://app.gitbook.com/s/FBsiDeuhN5SJcOCFJbtD/priv-esc) (Medjed)

</details>
