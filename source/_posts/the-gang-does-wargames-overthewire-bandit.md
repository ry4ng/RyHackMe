---
title: "The Gang Does Wargames: OverTheWire (Bandit)"
date: 2024-09-28 08:45:14
author: ['ry4ng']
tags: ['overthewire','bandit','wargames','linux','basics','ssh','walkthrough']
---

# OverTheWire - Bandit
Walkthrough for the [Bandit Wargame](https://overthewire.org/wargames/bandit/) on `OverTheWire.org`

*This is a dynamic blog post, with solutions being posted as they are completed.*

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