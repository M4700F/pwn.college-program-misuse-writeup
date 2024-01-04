```
'hd' means hexadecimal dump. It is used to display the contents of the file in hexadecimal format alongside with ASCII characters in this case
```

```
hacker@program-misuse-level-12:~$ cd /
hacker@program-misuse-level-12:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-12:/$ cd challenge/
hacker@program-misuse-level-12:/challenge$ ./babysuid_level12 
Welcome to ./babysuid_level12!

This challenge is part of a series of programs that
require you to understand their output to derive the flag from it.

I just set the SUID bit on /usr/bin/hd.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level12) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/hd!
hacker@program-misuse-level-12:/challenge$ hd /flag 
00000000  70 77 6e 2e 63 6f 6c 6c  65 67 65 7b 6b 68 4d 33  |pwn.college{khM3|
00000010  46 6f 70 46 71 76 49 52  38 48 58 53 64 4d 6a 61  |FopFqvIR8HXSdMja|
00000020  58 66 43 72 71 75 7a 2e  30 46 4e 31 45 44 4c 30  |XfCrquz.0FN1EDL0|
00000030  41 6a 4e 7a 51 7a 57 7d  0a                       |AjNzQzW}.|
00000039
```

```
The flag is
pwn.college{khM3FopFqvIR8HXSdMjaXfCrquz.0FN1EDL0AjNzQzW}
```