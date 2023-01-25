# Enumeration

### Ways To become Administrator&#x20;

* Reverse shells&#x20;
* Adding ourselves to the group
* PsExec

### Strat

1. whoami
2. net user \<username>
3. Privileges
4. run the local exploit suggester
5. Run winPEAS&#x20;
6. Run SeatBelt
7. Make a list of things you need to make the exploits work
8. Try to check passwords to RDP, runas
9. Check for user's Desktop and C:\ and C:\Program Files\\
10. Then look at exploitdb and searchsploit for possible exploits. literally look at everything please
11. Try things that dont require a lot first&#x20;
12. Check for ports running internally
13. Try Kernel Exploits



We can use accesschks and icacls to see permissions as well as dir /q /s to see ownership of files.

{% embed url="https://oscp.infosecsanyam.in/priv-escalation/windows-priv-escalation/checklist-local-windows-privilege-escalation" %}
