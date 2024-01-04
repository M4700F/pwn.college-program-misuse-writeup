
`rev` reverse the string.

```bash
hacker@program-misuse-level-10:~$ cd /
hacker@program-misuse-level-10:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-10:/$ cd challenge/
hacker@program-misuse-level-10:/challenge$ ls
babysuid_level10
hacker@program-misuse-level-10:/challenge$ ./babysuid_level10 
Welcome to ./babysuid_level10!

This challenge is part of a series of programs that
require you to understand their output to derive the flag from it.

I just set the SUID bit on /usr/bin/rev.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level10) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/rev!
hacker@program-misuse-level-10:/challenge$ ls -l /usr/bin/rev
-rwsr-xr-x 1 root root 14568 May 30  2023 /usr/bin/rev
hacker@program-misuse-level-10:/challenge$ 
hacker@program-misuse-level-10:/challenge$ 
hacker@program-misuse-level-10:/challenge$ rev /flag
}WzQzNjA0LDE1Ml0.Lvb4ZhZr3eBQIrfHvFwpk4gJrYs{egelloc.nwp
hacker@program-misuse-level-10:/challenge$ cat /flag
cat: /flag: Permission denied
hacker@program-misuse-level-10:/challenge$ g++ --version
g++ (Ubuntu 9.4.0-1ubuntu1~20.04.2) 9.4.0
Copyright (C) 2019 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

hacker@program-misuse-level-10:/challenge$ cd
hacker@program-misuse-level-10:~$ cd /
hacker@program-misuse-level-10:/$ rev flag | output.txt
bash: output.txt: command not found
hacker@program-misuse-level-10:/$ rev flag
}WzQzNjA0LDE1Ml0.Lvb4ZhZr3eBQIrfHvFwpk4gJrYs{egelloc.nwp
hacker@program-misuse-level-10:/$ rev flag > output.txt
bash: output.txt: Permission denied
hacker@program-misuse-level-10:/$ 
```

```
Now I searched online tool to reverse the string.

The flag is 
pwn.college{sYrJg4kpwFvHfrIQBe3rZhZ4bvL.0lM1EDL0AjNzQzW}
```