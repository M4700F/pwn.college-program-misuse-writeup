```bash
hacker@program-misuse-level-21:~$ cd /
hacker@program-misuse-level-21:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-21:/$ cd challenge/
hacker@program-misuse-level-21:/challenge$ ls
babysuid_level21
hacker@program-misuse-level-21:/challenge$ ./babysuid_level21 
Welcome to ./babysuid_level21!

This challenge is part of a series of programs that
force you to understand different archive formats.

I just set the SUID bit on /usr/bin/ar.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level21) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/ar!
hacker@program-misuse-level-21:/challenge$ cd ..
hacker@program-misuse-level-21:/$ ar flag
ar: invalid option -- 'g'
hacker@program-misuse-level-21:/$ ar r flag.a flag
ar: creating flag.a
hacker@program-misuse-level-21:/$ ls
bin  boot  challenge  dev  etc  flag  flag.a  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-21:/$ ar xp flag.a
ar: two different operation options specified
hacker@program-misuse-level-21:/$ ar p flag.a
pwn.college{kOQKWlMioMPHBbu_xQZ2-fRF6p7.01M2EDL0AjNzQzW}
```

`ar` is another unix utility to create, modify and extract from archive files `which specially focuses on libraries of object files.` don't know what does it mean :)

First I try `ar flag` but it shows error telling me that `invalid option`. That means that is not the correct way to archive files. I read the `man ar`. man is extremely useful.

Also run `ar --help`. This will show you only the necessary command you need. `man -` briefly describe the utilities which is often hard to find the necessary command.

I found a option `p` which `print files found in the archive`.

That prints the flag.