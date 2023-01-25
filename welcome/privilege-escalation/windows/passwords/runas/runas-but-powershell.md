# Runas but Powershell

![](https://i0.wp.com/steflan-security.com/wp-content/uploads/2021/05/image-102.png?w=800\&ssl=1)

It appears autologon credentials for the Alfred user are stored on the machine, the same credentials could possible have been used for the Administrator user:

![](https://i0.wp.com/steflan-security.com/wp-content/uploads/2021/05/image-103.png?w=800\&ssl=1)

Since there are no open services that would allow to remotely connect to the box as the Administrator user, such as RDP or WinRM, in order to exploit this, the PowerShell System.Management.Automation utility, which allows to execute scripts or binaries as a different user, can be leveraged. Clear-text credentials for the user can be provided when executing the command, which will be encrypted during execution.

Generating a reverse shell using MSFvenom with the following flags:

* \-p to specify the payload type, in this case, the Windows TCP Reverse Shelll
* LHOST to specify the localhost IP address to connect to
* LPORT to specify the local port to connect to
* \-f to specify the format for the shell, in this case, exe

![](https://i0.wp.com/steflan-security.com/wp-content/uploads/2021/05/image-104.png?w=800\&ssl=1)

Using the Certutil utility and the Python simple web server to transfer the reverse shell to the victim machine:

![](https://i0.wp.com/steflan-security.com/wp-content/uploads/2021/05/image-105.png?w=800\&ssl=1)

The next step is to set up a Netcat listener, which will catch the reverse shell when it is executed by the victim host, using the following flags:

* \-l to listen for incoming connections
* \-v for verbose output
* \-n to skip the DNS lookup
* \-p to specify the port to listen on

![](https://i0.wp.com/steflan-security.com/wp-content/uploads/2021/05/image-106.png?w=800\&ssl=1)

The following PowerShell command will execute the reverse shell as the Administrator user, if the credentials provided are correct:

```
powershell -c "$password = ConvertTo-SecureString 'Welcome1!' -AsPlainText -Force; $creds = New-Object System.Management.Automation.PSCredential('Administrator', $password);Start-Process -FilePath "shell.exe" -Credential $creds"
```

![](https://i0.wp.com/steflan-security.com/wp-content/uploads/2021/05/image-107.png?w=800\&ssl=1)

The command was executed successfully, confirming that the same credentials for Alfred were used for the Administrator user as well, and a callback on the Netcat listener was received, granting an administrative-level shell.
