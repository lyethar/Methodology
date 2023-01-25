# gcore SUID

According to&#x20;

{% embed url="https://gtfobins.github.io/gtfobins/gcore/" %}

{% embed url="https://wiki.sentnl.io/security/hacking-demos/getting-passwords-of-logged-in-users" %}

Gcore allows you to dump information about running processes, since this is running as root we are most likely able <mark style="color:red;">to dump information of processes that are runing as root.</mark> Maybe out of this we can use it get some sort of information. Linpeas will automatically tell you of the processes running as root.&#x20;

![](<../../../../.gitbook/assets/image (2).png>)

So we will dump the information of root processes using <mark style="color:green;">`sudo`</mark>` `<mark style="color:purple;">`gcore <`</mark>`pid`<mark style="color:purple;">`>`</mark>![](<../../../../.gitbook/assets/image (54).png>)![](<../../../../.gitbook/assets/image (61).png>)
