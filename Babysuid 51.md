`ssh-keygen`

`ssh-keygen` is a command line program that is used to generate SSH key pairs which are used for secure communication between two machine such as connecting to a remote server securely.

For this problem, these statements are very important.

```bash
Desktop  demo  key  key.pub
hacker@program-misuse-level-51:~$ /challenge/babysuid_level51 
Welcome to /challenge/babysuid_level51!

This challenge is part of a series of programs that
show you how dangerous it is to allow users to load their own code as plugins into the program (but figuring out how is the hard part!).

I just set the SUID bit on /usr/bin/ssh-keygen.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level51) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/ssh-keygen!
```

Here I think the problem wants us to load our code in the program here the program means `ssh-keygen`. 