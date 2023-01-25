# Python based applications escalation

If they run as root and we can write them replace them with a python reverse shell.&#x20;

### Module Hijacking

This happens when the module that a script wants to use isnt imported, we can replace it with our own version.&#x20;

| 1 | `sudo` `-l` |
| - | ----------- |

[![](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-18\_04-23.png?w=1024)](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-18\_04-23.png)

wifi\_reset.py was importing a module wificontroller and executing some commands but this wifcontroller module was absent.

[![](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-18\_04-25.png?w=716)](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-18\_04-25.png)

So ,we created our malicious **wificontroller.py** module inside the same folder i.e. **/home/walter** which had the malicious Privilege Escalation code. And executed it.

```python
import os
 
def stop(text,value):
        os.system("chmod 777 /etc/passwd");
 
def reset(text,value):
        os.system("chmod +s /bin/bash");
 
def start(text,value):
        os.system("chmod 777 /etc/shadow");
```

[![](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-18\_05-37.png?w=929)](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-18\_05-37.png)

As a result of executing it, we got following results.

[![](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-18\_05-38.png?w=809)](https://grumpygeekwrites.files.wordpress.com/2021/09/2021-09-18\_05-38.png)

BASH is having SUID bit. So, we became root with following command and read the root flag.

![](https://miro.medium.com/max/774/1\*pHwdVenZK2p10bkdlxBm3Q.png)

See? All it does it spawn a bash shell. Now lets run our sudo command “sudo /usr/bin/python /home/walter/wifi\_reset.py”.

![](https://miro.medium.com/max/1238/1\*z6wTAIRzU63oLG8hmf4RsQ.png)

We get root, proof.txt and this box is done.
