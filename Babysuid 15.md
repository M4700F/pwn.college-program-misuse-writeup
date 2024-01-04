```bash
hacker@program-misuse-level-15:~$ cd /
hacker@program-misuse-level-15:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-15:/$ cd challenge/
hacker@program-misuse-level-15:/challenge$ ls
babysuid_level15
hacker@program-misuse-level-15:/challenge$ ./babysuid_level15 
Welcome to ./babysuid_level15!

This challenge is part of a series of programs that
require you to understand their output to derive the flag from it.

I just set the SUID bit on /usr/bin/base64.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level15) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/base64!
hacker@program-misuse-level-15:/challenge$ base64 /flag 
cHduLmNvbGxlZ2V7b2tqd053NHllY3VuVmJIaGoxY0s5M2ZKYjBBLjAxTjFFREwwQWpOelF6V30K
```

```
Same approach like the previous ones. Use cyberchef 
pwn.college{okjwNw4yecunVbHhj1cK93fJb0A.01N1EDL0AjNzQzW}
```
