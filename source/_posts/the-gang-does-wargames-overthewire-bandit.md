---
title: "The Gang Does Wargames: OverTheWire - Bandit [Technical Walkthrough]"
date: 2024-09-28 08:45:14
author: ['ry4ng']
tags: ['overthewire','bandit','wargames','linux','basics','ssh', 'technical walkthrough']
---

# OverTheWire - Bandit
Walkthrough for the [Bandit Wargame](https://overthewire.org/wargames/bandit/) on `OverTheWire.org`

*This is a live blog post, with solutions being posted as they are completed.*

<!-- ## Table of Contents
1. [Level 0](#Level-0)
2. [Level 1](#Level-0-1)
3. [Level 2](#Level-1-2)
4. [Level 3](#Level-2-3) -->

## Level 0
> The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

1) SSH to server provided on port `2220` and use the credetnails provided to login. Once logged in, move onto the next level.
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
`-p` is used to specify the SSH port (default for SSH is `22`)

## Level 0>1
> The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game. 

1) Check for files on the host using `ls`
```bash
bandit0@bandit:~$ ls -l
total 4
-rw-r----- 1 bandit1 bandit0 438 Sep 19 07:08 readme
```
`-l` is used to list the files with some more information 

2) Read the file contents using `cat`
```
bandit0@bandit:~$ cat readme 
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

## Level 1>2 
> The password for the next level is stored in a file called - located in the home directory

1) To open a file with a `-` as a filename. You need to specify full path. 
```bash
bandit1@bandit:~$ cat ~/-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

## Level 2>3
> The password for the next level is stored in a file called spaces in this filename located in the home directory

1) Quotes can be used to open a file with spaces in the filename. 
```bash
bandit2@bandit:~$ cat "spaces in this filename" 
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

## Level 3>4
> The password for the next level is stored in a hidden file in the inhere directory.

1) Using `ls`, show all files within the a directory 
```bash
bandit3@bandit:~/inhere$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 Sep 19 07:08 .
drwxr-xr-x 3 root    root    4096 Sep 19 07:08 ..
-rw-r----- 1 bandit4 bandit3   33 Sep 19 07:08 ...Hiding-From-You
```
`-a` is used to show all files within a directory 

2) Read the file contents 
```bash
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

## Level 4>5
> The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

1) Check the contents of the `inhere` directory
```bash
bandit4@bandit:~/inhere$ ls -la
total 48
drwxr-xr-x 2 root    root    4096 Sep 19 07:08 .
drwxr-xr-x 3 root    root    4096 Sep 19 07:08 ..
-rw-r----- 1 bandit5 bandit4   33 Sep 19 07:08 -file00
-rw-r----- 1 bandit5 bandit4   33 Sep 19 07:08 -file01
-rw-r----- 1 bandit5 bandit4   33 Sep 19 07:08 -file02
-rw-r----- 1 bandit5 bandit4   33 Sep 19 07:08 -file03
-rw-r----- 1 bandit5 bandit4   33 Sep 19 07:08 -file04
-rw-r----- 1 bandit5 bandit4   33 Sep 19 07:08 -file05
-rw-r----- 1 bandit5 bandit4   33 Sep 19 07:08 -file06
-rw-r----- 1 bandit5 bandit4   33 Sep 19 07:08 -file07
-rw-r----- 1 bandit5 bandit4   33 Sep 19 07:08 -file08
-rw-r----- 1 bandit5 bandit4   33 Sep 19 07:08 -file09
```

2) The following command can be used to loop through all the files in the directory. Taking caution with the filenames starting with `-`
```bash
bandit4@bandit:~/inhere$ for file in ./*; do file $file; done
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```
`for file in ./*;` For each item that matches wildcard `*` in the current directory (`.` means current directory), assign it to the variable `file`, which can later be referenced as `$file`
`do file $file;` For each item, run the command `file` on it, this will display information about the contents of the file. 

3) From the output, there is only 1 file containing human-readable `ASCII` text. View the contents of this file. 
```bash
bandit4@bandit:~/inhere$ cat ./-file07 
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

## Level 5>6
> The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties: `human-readable`, `1033` bytes in size, `not executable`

1) Utilise the `find` command to search for the specific file
```bash
bandit5@bandit:~/inhere$ find -type f -not -executable -size 1033c -exec file '{}' \;
./maybehere07/.file2: ASCII text, with very long lines (1000)
```
`-type f` Look for files only.
`-not -executable` Used to negate the following flag or condition i.e. not executable.
`-size 1033c` Look for files of exactly size `1033` bytes. Further size suffixes below.
`-exec file '{}' \;` For each file found within the criteria, rune the `file` command agaisnt it. 
```
              `b'    for 512-byte blocks (this is the default if no suffix is used)
              `c'    for bytes
              `w'    for two-byte words
              `k'    for kibibytes (KiB, units of 1024 bytes)
              `M'    for mebibytes (MiB, units of 1024 * 1024 = 1048576 bytes)
              `G'    for gibibytes (GiB, units of 1024 * 1024 * 1024 = 1073741824 bytes)
```

2) Read the file contents 
```bash
$ cat ./inhere/maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

## Level 6>7
> The password for the next level is stored somewhere on the server and has all of the following properties: owned by user `bandit7`, owned by group `bandit6`, `33` bytes in size

1) Utilise the `find` command to search for the specific file
```bash
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2> /dev/null
/var/lib/dpkg/info/bandit7.password
```
`-user` Find items owned by a specific user 
`-group` Find items that belong to a specific group  
`2> /dev/null` Used to supresses errors (ensuring the console doens't become clogged with error messages, usually permission denied errors in this case)

2) Read the file contents 
```bash
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

## Level 7>8
> The password for the next level is stored in the file `data.txt` next to the word millionth

1) Utilise the `grep` command to search for the word within the file
*Learn more about `grep` courtesy of the gang [here](/RyHackMe/2024/09/28/The-Gang-Grapples-with-Grep/)*
```bash
bandit7@bandit:~$ cat data.txt | grep -i "millionth"
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```