```bash
hacker@program-misuse-level-9:~$ cd /
hacker@program-misuse-level-9:/$ cd challenge
hacker@program-misuse-level-9:/challenge$ ./babysuid_level9 
Welcome to ./babysuid_level9!

This challenge is part of a series of programs that
shows you that an over-privileged editor is a very powerful tool, indeed.

I just set the SUID bit on /usr/bin/nano.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level9) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/nano!
hacker@program-misuse-level-9:/challenge$ ls -l /usr/bin/nano
-rwsr-xr-x 1 root root 320136 Apr 10  2020 /usr/bin/nano
hacker@program-misuse-level-9:/challenge$ nano /flag
hacker@program-misuse-level-9:/challenge$ 
```


```
pwn.college{ck6RBvEkHx9xF_TZr8LnaukNyl4.0FM1EDL0AjNzQzW}
```