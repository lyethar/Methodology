# Enumerating SUID binaries

```
find / -perm -u=s -type f 2>/dev/nul
```

Look them up on gtfobins.
