# Glusterd + Docker Container Breakout

When looking at the processes i noticed [gluster](https://www.techtarget.com/searchstorage/definition/GlusterFS-Gluster-File-System) running.

![](https://miro.medium.com/max/700/1\*Plcmq87DZGLV\_-KLY8NWrw.png)

After some research i found gluster to be vulnerable to a local privilege escalation exploit: [cve-2018–1088](https://access.redhat.com/articles/3414511), this exploit will allow us to escape the docker container and fully compromise the machine.

To exploit cve-2018–1088 we basically mount a share to a share on the server containing the gcron\_enabled file and add a malicious cronjob that will execute a reverse shell on the main host.

![](https://miro.medium.com/max/334/1\*rhSFQKLwidsw8ZihiNa4zg.png)

creating the share to mount to the host

![](https://miro.medium.com/max/700/1\*aCSg9SCeP5SMPkIuOltTNA.png)

mounting the share through gluster

![](https://miro.medium.com/max/700/1\*o-SWxGcofiZlKrnRb8tU9g.png)creating the scheduled task to be executed![](https://miro.medium.com/max/700/1\*uG1M\_A6TRWEdtMlQOyVWtA.png)

creating the malicious payload![](https://miro.medium.com/max/688/1\*yRsadZFtKisC0KEOJ7cP3w.png)

cronjob downloading my malicious executable![](https://miro.medium.com/max/558/1\*AswIpnD47U1hLnGA-5yoOg.png)

gaining full compromise
