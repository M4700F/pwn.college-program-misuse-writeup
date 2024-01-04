```bash
hacker@program-misuse-level-14:~$ ls
Desktop
hacker@program-misuse-level-14:~$ cd /
hacker@program-misuse-level-14:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-14:/$ cd challenge/
hacker@program-misuse-level-14:/challenge$ ls
babysuid_level14
hacker@program-misuse-level-14:/challenge$ ./babysuid_level14 
Welcome to ./babysuid_level14!

This challenge is part of a series of programs that
require you to understand their output to derive the flag from it.

I just set the SUID bit on /usr/bin/base32.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level14) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/base32!
hacker@program-misuse-level-14:/challenge$ base32 /flag 
OB3W4LTDN5WGYZLHMV5W6WBXJVHTIV2IFUZVGRRSM5WVQWTGFV4GYTJNGRZTSZBOGBWE4MKFIRGD
AQLKJZ5FC6SXPUFA====
```

```
The flag is in base32. Go to cyberchef and decode it.
The flag is
pwn.college{oX7MO4WH-3SF2gmXZf-xlM-4s9d.0lN1EDL0AjNzQzW}
```