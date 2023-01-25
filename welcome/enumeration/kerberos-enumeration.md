# Kerberos Enumeration

### Kerbrute

{% embed url="https://github.com/insidetrust/statistically-likely-usernames" %}

I had 2 different version of kerbrute that work different so I will label them differently&#x20;

Validating Users&#x20;

```
kerbrute2 userenum --dc 10.10.10.172 -d MEGABANK.LOCAL userlist2
```

Validating Users and taking TGTs if they dont have preauth.

```
kerbrute -domain intelligence.htb -users userlist
```
