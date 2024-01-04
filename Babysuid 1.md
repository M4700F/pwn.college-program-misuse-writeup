> [!NOTE]
> What is `SUID`?
> 
> `SUID` stands for set user ID. Every process has a user ID. When the process's `UID` is 0 that means that process is executed by the root user. In this whole module, you will see some command has been `SUID` that means you can run those command using `root` privileges. That means you become a `pseudo-root` for that specific command. That command will treat you as the `root `user.


```bash
hacker@program-misuse-level-1:~$ 
hacker@program-misuse-level-1:~$ ls
Desktop
hacker@program-misuse-level-1:~$ pwd
/home/hacker
hacker@program-misuse-level-1:~$ cd /
hacker@program-misuse-level-1:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-1:/$ file flag
flag: regular file, no read permission
hacker@program-misuse-level-1:/$ cat flag
cat: flag: Permission denied
hacker@program-misuse-level-1:/$ ls -l flag
-r-------- 1 root root 57 Dec 30 16:01 flag
hacker@program-misuse-level-1:/$ which cat
/usr/bin/cat
hacker@program-misuse-level-1:/$ ls -l /usr/bin/cat
-rwxr-xr-x 1 root root 43416 Sep  5  2019 /usr/bin/cat
hacker@program-misuse-level-1:/$ sudo cat flag
sudo: /usr/bin/sudo must be owned by uid 0 and have the setuid bit set
hacker@program-misuse-level-1:/$ 
hacker@program-misuse-level-1:/$ 
hacker@program-misuse-level-1:/$ cd challenge
hacker@program-misuse-level-1:/challenge$ ls
babysuid_level1
hacker@program-misuse-level-1:/challenge$ ./babysuid_level1 
Welcome to ./babysuid_level1!

This challenge is part of a series of programs that
exposes you to very simple programs that let you directly read the flag.

I just set the SUID bit on /usr/bin/cat.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level1) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/cat!
hacker@program-misuse-level-1:/challenge$ 
hacker@program-misuse-level-1:/challenge$ 
hacker@program-misuse-level-1:/challenge$ ls -l /usr/bin/cat
-rwsr-xr-x 1 root root 43416 Sep  5  2019 /usr/bin/cat
hacker@program-misuse-level-1:/challenge$ cat /flag
pwn.college{MqIgJ8DHc0Sn7LGY7bEIjvYWBTd.01M0EDL0AjNzQzW}
```

At first you can see the when I run `cat flag` it says `permission denied`. That means I don't have the necessary privileges to read the file. You can see that if you run `ls -l flag` , only `root` can read the file. 

Now if I run the executable in the `/challenge/babysuid_level1` , then the `SUID` has been set for the `cat` command. The `cat` command will think that I am the `root`. Then I can `cat` the flag.