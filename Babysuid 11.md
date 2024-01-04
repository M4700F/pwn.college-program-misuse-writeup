```
'od' means octal dump. It is used to display the contents of file in a octal format.
```

```bash
hacker@program-misuse-level-11:~$ ls
Desktop
hacker@program-misuse-level-11:~$ cd /
hacker@program-misuse-level-11:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-11:/$ cd challenge/
hacker@program-misuse-level-11:/challenge$ ls
babysuid_level11
hacker@program-misuse-level-11:/challenge$ ./babysuid_level11 
Welcome to ./babysuid_level11!

This challenge is part of a series of programs that
require you to understand their output to derive the flag from it.

I just set the SUID bit on /usr/bin/od.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level11) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/od!
hacker@program-misuse-level-11:/challenge$ od /flag
0000000 073560 027156 067543 066154 063545 075545 067147 047102
0000020 043067 030537 041462 042122 067542 061127 026503 032514
0000040 067542 030103 041124 027114 030460 030515 042105 030114
0000060 065101 075116 075121 076527 000012
0000071
hacker@program-misuse-level-11:/challenge$ od -c /flag
0000000   p   w   n   .   c   o   l   l   e   g   e   {   g   n   B   N
0000020   7   F   _   1   2   C   R   D   b   o   W   b   C   -   L   5
0000040   b   o   C   0   T   B   L   .   0   1   M   1   E   D   L   0
0000060   A   j   N   z   Q   z   W   }  \n
0000071
```

```
Then I copy that flag portion and edit it in a text editor
and removing the spaces. But it will take time and there are chances to make mistake.
```

```
We can automate this thing with 'sed' command. But I don't know how to do it. Probably will learn later.
```

```
The easiest way is to ask gpt.

"0000000 p w n . c o l l e g e { g n B N 0000020 7 F _ 1 2 C R D b o W b C - L 5 0000040 b o C 0 T B L . 0 1 M 1 E D L 0 0000060 A j N z Q z W } nl 0000071 
give me the string without spaces"

Removing the spaces, the string reads:

pwn.college{gnBN7F_12CRDboWbC-L5boC0TBL.01M1EDL0AjNzQzW}nl

That's the flag!
```
