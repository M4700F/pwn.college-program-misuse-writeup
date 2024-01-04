```bash
hacker@program-misuse-level-2:~$ ls
Desktop
hacker@program-misuse-level-2:~$ cd /
hacker@program-misuse-level-2:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-2:/$ cat flag
cat: flag: Permission denied
hacker@program-misuse-level-2:/$ ls -l flag
-r-------- 1 root root 57 Dec 30 16:13 flag
hacker@program-misuse-level-2:/$ cd challenge/
hacker@program-misuse-level-2:/challenge$ ls
babysuid_level2
hacker@program-misuse-level-2:/challenge$ ./babysuid_level2 
Welcome to ./babysuid_level2!

This challenge is part of a series of programs that
exposes you to very simple programs that let you directly read the flag.

I just set the SUID bit on /usr/bin/more.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level2) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/more!
hacker@program-misuse-level-2:/challenge$ more /flag
pwn.college{g6zLG_TRi7XJ0AAGh7Y2Ueb80GN.0FN0EDL0AjNzQzW}
hacker@program-misuse-level-2:/challenge$ 
```