# 👁🗨 Enumeration Cheatsheet

### Autorecon Multi-Target Scan

#### **Multi-Target Scan**

By default, AutoRecon will scan 5 target hosts at the same time but that number can be toggled using the -ct parameter. This is basically the number of targets getting scanned at the same time. To demonstrate, we collected some IP Address in the network and then entered them into a text file. Then used that text file to provide targets to AutoRecon.

```
cat target.txt
autorecon -t targets.txt
```

![](https://i0.wp.com/1.bp.blogspot.com/-wfXbq8UoRxY/YFtTJJJO4EI/AAAAAAAAu8w/OVCziimImWAi40iR1ToZAHuYe8o3lW2QQCLcBGAsYHQ/s16000/8.png?w=640\&ssl=1)

### TCP

Windows all ports:

```
nmap -Pn -p- --open -sS --min-rate 5000 -vvv -n IP
```

#### UDP

```
nmap -sUV -T4 -F --version-intensity 0 IP
```

### Little NMAP CheatSheet

```
The Basic Scan

By default Nmap does a standard TCP SYN scan on the top 1000 ports of host. I never really use this by itself.



$ nmap host

At an absolute minimum, I will get more verbosity using -v or -vv.



$ nmap -vv host

Target Specification

Nmap accepts target specification in loads of different formats including plain IP addresses, CIDR ranges and dash notation.



$ nmap hostname

$ nmap 123.123.123.123

$ nmap 123.123.123.1/24

$ nmap 123.123.123.1–255

Ping Sweeping

If you just want to find which hosts are alive, you can perform a ping scan with -sn



$ nmap -sn 123.123.123.1/24

Sometimes, hosts don’t respond to ping. To skip ping checks and just scan the host ports anyway, use -Pn:



$ nmap -Pn host

Scan Targets in a File

To scan a list of hosts from a file, use -iL:



$ nmap -iL ./hosts.txt

Scan Types

There are 9 scan types. The main 2 that you will use are:



TCP SYN (-sS)

UDP (-sU)

The default scan type is TCP SYN. To scan UDP ports use -sU. Other scan types can be useful for stealth or probing firewalls but may sacrifice accuracy or speed. You can find more information about the different nmap scan types here: https://nmap.org/book/man-port-scanning-techniques.html



Specifying Ports

You can specify which ports to scan with -p. By default, only 1000 ports are scanned. To scan all ports:



$ nmap -p 1–65535 host

Protip: To scan all ports you can also use nmap -p- host, which is shorthand for nmap -p 1–65535 host.



You can also specify a comma separated list with single ports, ranges and specific UDP ports:



$ nmap -p 23,23,25,110,80–90,U:53,1000–2000

Version and OS Enumeration

When Nmap finds an open port it can probe further to discover what service it is running if you specify -sV. You can set how intense you want the probes to be from 0 (light probe, fast but not accurate) to 9 (try all probes, slow but accurate)



$ nmap -sV — version-intensity 9

Nmap can guess which operating system a host is running based the scan results. Enable this feature with -O:



$ nmap -O host

Firewall Evasion

It also has extensive firewall evasion functionality. I’ve honestly never used these features but they allow you to do some cool things including spoofing the source address.



Output Formats

Nmap offers many output formats. Some are better for humans to read, others are better for parsing into other tools. I tend to output scans into all formats using:



$ nmap -oA outputfile host

Specific options include:



-oN Normal

-oX XML

-oS scr1pt k1dd13

-oG greppable

Scan Speed

You can also adjust the speed that nmap scans at. using -T<0–5>. A higher number means a higher speed.



Higher speed means less accuracy, and vice versa.



$ nmap -T3 host

Nmap Scripting Engine

This is where Nmap gets really interesting! It can also run Lua scripts. These can do pretty much anything. Nmap comes with about 600 of them that perform various vuln scanning and enumeration tasks, but you can also code your own.



The location of Lua scripts is:



<nmap directory>/share/nmap/scripts/*

Depending on your setup, you might also find them by running:



$ locate *.nse

As an example of using Nmap scripts, to check if a host is vulnerable to Eternal Blue, you could run:



$ nmap --script=smb-vuln-cve-2017–7494 host

Some scripts require arguments, you can specify them with --script-args=n1=v1,n2=v2 etc.



To get help on which arguments may be accepted by a script:



$ nmap --script-help=scriptname

To upgrade your scripts to the latest and greatest, just run:



$ nmap --script-updatedb

A Nice Alias -A

A helpful alias is -A, which will enable OS detection, service version detection, script scanning, and traceroute.



nmap -A host

My Go-To Command

For a thorough scan of a single host, a decent go-to command is:



$ nmap -A -p1–65535 -v host
```
