```bash
hacker@program-misuse-level-6:~$ cd /
hacker@program-misuse-level-6:/$ cd challenge/
hacker@program-misuse-level-6:/challenge$ ls
babysuid_level6
hacker@program-misuse-level-6:/challenge$ ./babysuid_level6 
Welcome to ./babysuid_level6!

This challenge is part of a series of programs that
exposes you to very simple programs that let you directly read the flag.

I just set the SUID bit on /usr/bin/sort.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level6) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/sort!
hacker@program-misuse-level-6:/challenge$ sort /flag
pwn.college{Ulv2_DV8GZGT-bNliKu1uPcU5Yp.0FO0EDL0AjNzQzW}
hacker@program-misuse-level-6:/challenge$ 

```