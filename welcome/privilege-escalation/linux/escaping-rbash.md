# Escaping RBASH

I will give differnt methods that you should try.&#x20;

### Method 1&#x20;

```
BASH_CMDS[a]=/bin/sh;a
export PATH=$PATH:/bin/
export PATH=$PATH:/usr/bin
```

### Method 2&#x20;

{% embed url="https://www.metahackers.pro/breakout-of-restricted-shell/" %}

Try everything in this article.&#x20;

### Method 3&#x20;

The last method is one I encoutered in Peppo from Proving Grounds. By enumerating the $PATH environment variable we could see where the binaries are run from.&#x20;

```
echo $PATH 
```

Based on the $PATH directory we can list the binaries that the user can run.&#x20;

```
$ ls bin

chmod chwon ed ls mv ping sleep touch 
```

Now based on those binaries that we can run, these could be used to break out of restricte environments.&#x20;

Look them up in gtfobins.&#x20;

{% embed url="https://gtfobins.github.io/gtfobins/ed/" %}

In this case we see that there is binary called "ed " and once we look that binary up we see that the binary ed can be used to break out of instances.&#x20;
