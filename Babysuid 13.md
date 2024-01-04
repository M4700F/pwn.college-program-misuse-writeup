```
'xxd' is another command for viewing hex dump of a file similar to 'hd'. But 'xxd' has more functionality than 'hd'. It gives more flexibilty.
```

```bash
hacker@program-misuse-level-13:~$ ls
Desktop
hacker@program-misuse-level-13:~$ cd /
hacker@program-misuse-level-13:/$ cd challenge/
hacker@program-misuse-level-13:/challenge$ ls
babysuid_level13
hacker@program-misuse-level-13:/challenge$ ./babysuid_level13 
Welcome to ./babysuid_level13!

This challenge is part of a series of programs that
require you to understand their output to derive the flag from it.

I just set the SUID bit on /usr/bin/xxd.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level13) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/xxd!
hacker@program-misuse-level-13:/challenge$ xxd /flag 
00000000: 7077 6e2e 636f 6c6c 6567 657b 3458 6673  pwn.college{4Xfs
00000010: 6d65 4858 3044 7372 696c 4c68 6e75 6441  meHX0DsrilLhnudA
00000020: 3256 4733 5942 722e 3056 4e31 4544 4c30  2VG3YBr.0VN1EDL0
00000030: 416a 4e7a 517a 577d 0a                   AjNzQzW}.
```

```
The flag is:
pwn.college{4XfsmeHX0DsrilLhnudA2VG3YBr.0VN1EDL0AjNzQzW}
```