## Bandit

The Bandit wargame is aimed at absolute beginners. It will teach the basics needed to be able to play other wargames.

**If you notice something essential is missing or have ideas for new levels, please let us know!**

#### Note for beginners

This game, like most other games, is organised in levels. You start at Level 0 and try to “beat” or “finish” it. Finishing a level results in information on how to start the next level. The pages on this website for “Level <X>” contain information on how to start level X from the previous level. E.g. The page for Level 1 has information on how to gain access from Level 0 to Level 1. All levels in this game have a page on this website, and they are all linked to from the sidemenu on the left of this page.

You will encounter many situations in which you have no idea what you are supposed to do. **Don’t panic! Don’t give up!** The purpose of this game is for you to learn the basics. Part of learning the basics, is reading a lot of new information.

There are several things you can try when you are unsure how to continue:

First, if you know a command, but don’t know how to use it, try the manual (man page) by entering **“man <command>”** (without the quotes). e.g. if you know about the “ls” command, type: man ls. The “man” command also has a manual, try it. Press q to quit the man command.
Second, if there is no man page, the command might be a **shell built-in** In that case use the **“help <X>”** command. E.g. help cd
Also, your favorite **search-engine** is your friend. Learn how to use it! I recommend Google.
Lastly, if you are still stuck, you can join us via chat

You’re ready to start! Begin with Level 0, linked at the left of this page. Good luck!

**Note for VMs:** You may fail to connect to overthewire.org via SSH with a “**broken pipe error**” when the network adapter for the VM is configured to use NAT mode. Adding the setting IPQoS throughput to `/etc/ssh/ssh_config` should resolve the issue. If this does not solve your issue, the only option then is to change the adapter to Bridged mode.

### Level 0

#### Level Goal

The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

#### Commands you may need to solve this level

ssh

#### Helpful Reading Material

Secure Shell (SSH) on Wikipedia
How to use SSH on wikiHow

---

### Level 0 - Level 1

#### Level Goal

The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

#### Commands you may need to solve this level

ls, cd, cat, file, du, find

```
bandit0@bandit:~$ ls -la
total 24
drwxr-xr-x  2 root    root    4096 May  7  2020 .
drwxr-xr-x 41 root    root    4096 May  7  2020 ..
-rw-r--r--  1 root    root     220 May 15  2017 .bash_logout
-rw-r--r--  1 root    root    3526 May 15  2017 .bashrc
-rw-r--r--  1 root    root     675 May 15  2017 .profile
-rw-r-----  1 bandit1 bandit0   33 May  7  2020 readme
bandit0@bandit:~$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
bandit0@bandit:~$

```

---

### Level 1 - Level 2

#### Level Goal

The password for the next level is stored in a file called - located in the home directory
Commands you may need to solve this level

ls, cd, cat, file, du, find

#### Helpful Reading Material

Google Search for “dashed filename”
Advanced Bash-scripting Guide - Chapter 3 - Special Characters

```
bandit1@bandit:~$ ls -la
total 24
-rw-r-----  1 bandit2 bandit1   33 May  7  2020 -
drwxr-xr-x  2 root    root    4096 May  7  2020 .
drwxr-xr-x 41 root    root    4096 May  7  2020 ..
-rw-r--r--  1 root    root     220 May 15  2017 .bash_logout
-rw-r--r--  1 root    root    3526 May 15  2017 .bashrc
-rw-r--r--  1 root    root     675 May 15  2017 .profile
bandit1@bandit:~$ cat ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
bandit1@bandit:~$
```

---

### Level 2 - Level 3

#### Level Goal

The password for the next level is stored in a file called spaces in this filename located in the home directory

#### Commands you may need to solve this level

ls, cd, cat, file, du, find

#### Helpful Reading Material

Google Search for “spaces in filename”

```
bandit2@bandit:~$ ls -la
total 24
drwxr-xr-x  2 root    root    4096 May  7  2020 .
drwxr-xr-x 41 root    root    4096 May  7  2020 ..
-rw-r--r--  1 root    root     220 May 15  2017 .bash_logout
-rw-r--r--  1 root    root    3526 May 15  2017 .bashrc
-rw-r--r--  1 root    root     675 May 15  2017 .profile
-rw-r-----  1 bandit3 bandit2   33 May  7  2020 spaces in this filename
bandit2@bandit:~$ cat spaces\ in\ this\ filename
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
bandit2@bandit:~$

```

---

### Level 3 - Level 4

#### Level Goal

The password for the next level is stored in a hidden file in the inhere directory.

#### Commands you may need to solve this level

ls, cd, cat, file, du, find

```
bandit3@bandit:~$ ls -la
total 24
drwxr-xr-x  3 root root 4096 May  7  2020 .
drwxr-xr-x 41 root root 4096 May  7  2020 ..
-rw-r--r--  1 root root  220 May 15  2017 .bash_logout
-rw-r--r--  1 root root 3526 May 15  2017 .bashrc
drwxr-xr-x  2 root root 4096 May  7  2020 inhere
-rw-r--r--  1 root root  675 May 15  2017 .profile
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 May  7  2020 .
drwxr-xr-x 3 root    root    4096 May  7  2020 ..
-rw-r----- 1 bandit4 bandit3   33 May  7  2020 .hidden
bandit3@bandit:~/inhere$ cat .hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
bandit3@bandit:~/inhere$

```

---

### Level 4 - Level 5

#### Level Goal

The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

#### Commands you may need to solve this level

ls, cd, cat, file, du, find

```

bandit4@bandit:~$ ls -la
total 24
drwxr-xr-x  3 root root 4096 May  7  2020 .
drwxr-xr-x 41 root root 4096 May  7  2020 ..
-rw-r--r--  1 root root  220 May 15  2017 .bash_logout
-rw-r--r--  1 root root 3526 May 15  2017 .bashrc
drwxr-xr-x  2 root root 4096 May  7  2020 inhere
-rw-r--r--  1 root root  675 May 15  2017 .profile
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls -la
total 48
drwxr-xr-x 2 root    root    4096 May  7  2020 .
drwxr-xr-x 3 root    root    4096 May  7  2020 ..
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file00
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file01
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file02
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file03
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file04
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file05
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file06
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file07
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file08
-rw-r----- 1 bandit5 bandit4   33 May  7  2020 -file09
bandit4@bandit:~/inhere$ xargs
^C
bandit4@bandit:~/inhere$
bandit4@bandit:~/inhere$ for x in {0..9}; do file ./-file0$x; done;
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
bandit4@bandit:~/inhere$ cat ./-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
bandit4@bandit:~/inhere$

```

---

### Level 5 - Level 6

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

- human-readable
- 1033 bytes in size
- not executable

Commands you may need to solve this level

ls, cd, cat, file, du, find

```
bandit5@bandit:~$ ls -la
total 24
drwxr-xr-x  3 root root    4096 May  7  2020 .
drwxr-xr-x 41 root root    4096 May  7  2020 ..
-rw-r--r--  1 root root     220 May 15  2017 .bash_logout
-rw-r--r--  1 root root    3526 May 15  2017 .bashrc
drwxr-x--- 22 root bandit5 4096 May  7  2020 inhere
-rw-r--r--  1 root root     675 May 15  2017 .profile
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ ls -la
total 88
drwxr-x--- 22 root bandit5 4096 May  7  2020 .
drwxr-xr-x  3 root root    4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere00
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere01
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere02
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere03
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere04
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere05
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere06
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere07
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere08
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere09
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere10
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere11
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere12
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere13
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere14
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere15
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere16
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere17
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere18
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere19
bandit5@bandit:~/inhere$ find . -size 1033 c
find: paths must precede expression: c
Try 'find --help' for more information.
bandit5@bandit:~/inhere$ find . -size 1033c
./maybehere07/.file2
bandit5@bandit:~/inhere$ cd maybehere07
bandit5@bandit:~/inhere/maybehere07$ ls -la
total 56
drwxr-x---  2 root bandit5 4096 May  7  2020 .
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
-rwxr-x---  1 root bandit5 3663 May  7  2020 -file1
-rwxr-x---  1 root bandit5 3065 May  7  2020 .file1
-rw-r-----  1 root bandit5 2488 May  7  2020 -file2
-rw-r-----  1 root bandit5 1033 May  7  2020 .file2
-rwxr-x---  1 root bandit5 3362 May  7  2020 -file3
-rwxr-x---  1 root bandit5 1997 May  7  2020 .file3
-rwxr-x---  1 root bandit5 4130 May  7  2020 spaces file1
-rw-r-----  1 root bandit5 9064 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 1022 May  7  2020 spaces file3
bandit5@bandit:~/inhere/maybehere07$ cat .file2
DXjZPULLxYr17uwoI01bNLQbtFemEgo7

```

---

### Level 6 - Level 7

#### Level Goal

The password for the next level is stored somewhere on the server and has all of the following properties:

- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

#### Commands you may need to solve this level

ls, cd, cat, file, du, find, grep

```
bandit6@bandit:~$ find / -size 33c -user bandit7 -group bandit6 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$

bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
bandit6@bandit:~$

```

---

### Bandit Level 7 → Level 8

#### Level Goal

The password for the next level is stored in the file data.txt next to the word millionth

#### Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

```
bandit7@bandit:~$ ls -la
total 4108
drwxr-xr-x  2 root    root       4096 May  7  2020 .
drwxr-xr-x 41 root    root       4096 May  7  2020 ..
-rw-r--r--  1 root    root        220 May 15  2017 .bash_logout
-rw-r--r--  1 root    root       3526 May 15  2017 .bashrc
-rw-r-----  1 bandit8 bandit7 4184396 May  7  2020 data.txt
-rw-r--r--  1 root    root        675 May 15  2017 .profile
bandit7@bandit:~$ cat data.txt | grep millionth
millionth       cvX2JJa4CFALtqS87jk27qwqGhBM9plV
bandit7@bandit:~$

```

---

### Bandit Level 8 → Level 9

#### Level Goal

- The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

#### Commands you may need to solve this level

- grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

#### Helpful Reading Material

- Piping and Redirection

```
bandit8@bandit:~$ cat data.txt | sort | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
bandit8@bandit:~$

```

---

### Bandit Level 9 → Level 10

#### Level Goal

The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

#### Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

```
bandit9@bandit:~$ ls -la
total 40
drwxr-xr-x  2 root     root     4096 May  7  2020 .
drwxr-xr-x 41 root     root     4096 May  7  2020 ..
-rw-r--r--  1 root     root      220 May 15  2017 .bash_logout
-rw-r--r--  1 root     root     3526 May 15  2017 .bashrc
-rw-r-----  1 bandit10 bandit9 19379 May  7  2020 data.txt
-rw-r--r--  1 root     root      675 May 15  2017 .profile
bandit9@bandit:~$ cat data.txt | strings | grep "="
========== the*2i"4
=:G e
========== password
<I=zsGi
Z)========== is
A=|t&E
Zdb=
c^ LAh=3G
*SF=s
&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
S=A.H&^
bandit9@bandit:~$

```

### Bandit Level 10 → Level 11

#### Level Goal

The password for the next level is stored in the file data.txt, which contains base64 encoded data

#### Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

#### Helpful Reading Material

Base64 on Wikipedia

```
bandit10@bandit:~$ ls -la
total 24
drwxr-xr-x  2 root     root     4096 May  7  2020 .
drwxr-xr-x 41 root     root     4096 May  7  2020 ..
-rw-r--r--  1 root     root      220 May 15  2017 .bash_logout
-rw-r--r--  1 root     root     3526 May 15  2017 .bashrc
-rw-r-----  1 bandit11 bandit10   69 May  7  2020 data.txt
-rw-r--r--  1 root     root      675 May 15  2017 .profile
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==
bandit10@bandit:~$ cat data.txt | base64 -d
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
bandit10@bandit:~$

```

### Bandit Level 11 → Level 12

#### Level Goal

The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

#### Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

#### Helpful Reading Material

Rot13 on Wikipedia

```
bandit11@bandit:~$ ls -la
total 24
drwxr-xr-x  2 root     root     4096 May  7  2020 .
drwxr-xr-x 41 root     root     4096 May  7  2020 ..
-rw-r--r--  1 root     root      220 May 15  2017 .bash_logout
-rw-r--r--  1 root     root     3526 May 15  2017 .bashrc
-rw-r-----  1 bandit12 bandit11   49 May  7  2020 data.txt
-rw-r--r--  1 root     root      675 May 15  2017 .profile
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh
bandit11@bandit:~$ rot13
-bash: rot13: command not found
bandit11@bandit:~$ cat data.txt |  tr '[A-Za-z]' '[N-ZA-Mn-za-m]'
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
bandit11@bandit:~$

```

---

### Bandit Level 12 → Level 13

#### Level Goal

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

#### Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd, mkdir, cp, mv, file

#### Helpful Reading Material

Hex dump on

```
bandit12@bandit:/tmp/eagle$ ls
data2.txt  data.txt
bandit12@bandit:/tmp/eagle$ mv data2.txt hexdump
bandit12@bandit:/tmp/eagle$ ls -la
total 2000
drwxr-sr-x 2 bandit12 root    4096 Oct  2 07:45 .
drwxrws-wt 1 root     root 2031616 Oct  2 07:45 ..
-rw-r----- 1 bandit12 root    2582 Oct  2 07:35 data.txt
-rw-r--r-- 1 bandit12 root     606 Oct  2 07:44 hexdump
bandit12@bandit:/tmp/eagle$ file hexdump
hexdump: gzip compressed data, was "data2.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
bandit12@bandit:/tmp/eagle$ mv hexdump hexdump.gz
bandit12@bandit:/tmp/eagle$ gzip -d hexdump.gz
bandit12@bandit:/tmp/eagle$ ls -la
total 2000
drwxr-sr-x 2 bandit12 root    4096 Oct  2 07:47 .
drwxrws-wt 1 root     root 2031616 Oct  2 07:47 ..
-rw-r----- 1 bandit12 root    2582 Oct  2 07:35 data.txt
-rw-r--r-- 1 bandit12 root     573 Oct  2 07:44 hexdump
bandit12@bandit:/tmp/eagle$ file hexdump
hexdump: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/eagle$ mv hexdump hexdump.bz2
bandit12@bandit:/tmp/eagle$ bzip2 -d hexdump.bz2
bandit12@bandit:/tmp/eagle$ ls -la
total 2000
drwxr-sr-x 2 bandit12 root    4096 Oct  2 07:48 .
drwxrws-wt 1 root     root 2031616 Oct  2 07:48 ..
-rw-r----- 1 bandit12 root    2582 Oct  2 07:35 data.txt
-rw-r--r-- 1 bandit12 root     431 Oct  2 07:44 hexdump
bandit12@bandit:/tmp/eagle$ file hexdump
hexdump: gzip compressed data, was "data4.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
bandit12@bandit:/tmp/eagle$ mv hexdump hexdump.gz
bandit12@bandit:/tmp/eagle$ gzip -d hexdump.gz
bandit12@bandit:/tmp/eagle$ ls -la
total 2016
drwxr-sr-x 2 bandit12 root    4096 Oct  2 07:49 .
drwxrws-wt 1 root     root 2031616 Oct  2 07:49 ..
-rw-r----- 1 bandit12 root    2582 Oct  2 07:35 data.txt
-rw-r--r-- 1 bandit12 root   20480 Oct  2 07:44 hexdump
bandit12@bandit:/tmp/eagle$ file hexdump
hexdump: POSIX tar archive (GNU)
bandit12@bandit:/tmp/eagle$ tar -xvf hexdump
data5.bin
bandit12@bandit:/tmp/eagle$ file data5.bin
data5.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/eagle$ tar -xvf data5.bin
data6.bin
bandit12@bandit:/tmp/eagle$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/eagle$ mv data6.bin data6.bin.bz2
bandit12@bandit:/tmp/eagle$ bzip2 -d data6.bin.bz2
bandit12@bandit:/tmp/eagle$ ls
data5.bin  data6.bin  data.txt  hexdump
bandit12@bandit:/tmp/eagle$ file data6.bin
data6.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/eagle$ tar -xvf data6.bin
data8.bin
bandit12@bandit:/tmp/eagle$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
bandit12@bandit:/tmp/eagle$ gzip -d data8.bin
gzip: data8.bin: unknown suffix -- ignored
bandit12@bandit:/tmp/eagle$ ls
data5.bin  data6.bin  data8.bin  data.txt  hexdump
bandit12@bandit:/tmp/eagle$ mv data8.bin data8.bin.gz
bandit12@bandit:/tmp/eagle$ gzip -d data8.bin.gz
bandit12@bandit:/tmp/eagle$ ls -la
total 2044
drwxr-sr-x 2 bandit12 root    4096 Oct  2 07:54 .
drwxrws-wt 1 root     root 2031616 Oct  2 07:54 ..
-rw-r--r-- 1 bandit12 root   10240 May  7  2020 data5.bin
-rw-r--r-- 1 bandit12 root   10240 May  7  2020 data6.bin
-rw-r--r-- 1 bandit12 root      49 May  7  2020 data8.bin
-rw-r----- 1 bandit12 root    2582 Oct  2 07:35 data.txt
-rw-r--r-- 1 bandit12 root   20480 Oct  2 07:44 hexdump
bandit12@bandit:/tmp/eagle$ file data8.bin
data8.bin: ASCII text
bandit12@bandit:/tmp/eagle$ cat data8.bin
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
bandit12@bandit:/tmp/eagle$

```

---

### Bandit Level 13 → Level 14

#### Level Goal

The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

#### Commands you may need to solve this level

ssh, telnet, nc, openssl, s_client, nmap

#### Helpful Reading Material

SSH/OpenSSH/Keys

```
bandit13@bandit:~$ ls -la
total 24
drwxr-xr-x  2 root     root     4096 May  7  2020 .
drwxr-xr-x 41 root     root     4096 May  7  2020 ..
-rw-r--r--  1 root     root      220 May 15  2017 .bash_logout
-rw-r--r--  1 root     root     3526 May 15  2017 .bashrc
-rw-r--r--  1 root     root      675 May 15  2017 .profile
-rw-r-----  1 bandit14 bandit13 1679 May  7  2020 sshkey.private
bandit13@bandit:~$ cat sshkey.private
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
bandit13@bandit:~$

```

---

### Bandit Level 14 → Level 15

#### Level Goal

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

#### Commands you may need to solve this level

ssh, telnet, nc, openssl, s_client, nmap

#### Helpful Reading Material

- How the Internet works in 5 minutes (YouTube) (Not completely accurate, but good enough for beginners)
- IP Addresses
- IP Address on Wikipedia
- Localhost on Wikipedia
- Ports
- Port (computer networking) on Wikipedia

```
bandit14@bandit:/etc$ cd bandit_pass/
bandit14@bandit:/etc/bandit_pass$ ls -la
total 144
drwxr-xr-x  2 root     root     4096 May  7  2020 .
drwxr-xr-x 87 root     root     4096 May 14  2020 ..
-r--------  1 bandit0  bandit0     8 May  7  2020 bandit0
-r--------  1 bandit1  bandit1    33 May  7  2020 bandit1
-r--------  1 bandit10 bandit10   33 May  7  2020 bandit10
-r--------  1 bandit11 bandit11   33 May  7  2020 bandit11
-r--------  1 bandit12 bandit12   33 May  7  2020 bandit12
-r--------  1 bandit13 bandit13   33 May  7  2020 bandit13
-r--------  1 bandit14 bandit14   33 May  7  2020 bandit14
-r--------  1 bandit15 bandit15   33 May  7  2020 bandit15
-r--------  1 bandit16 bandit16   33 May  7  2020 bandit16
-r--------  1 bandit17 bandit17   33 May  7  2020 bandit17
-r--------  1 bandit18 bandit18   33 May  7  2020 bandit18
-r--------  1 bandit19 bandit19   33 May  7  2020 bandit19
-r--------  1 bandit2  bandit2    33 May  7  2020 bandit2
-r--------  1 bandit20 bandit20   33 May  7  2020 bandit20
-r--------  1 bandit21 bandit21   33 May  7  2020 bandit21
-r--------  1 bandit22 bandit22   33 May  7  2020 bandit22
-r--------  1 bandit23 bandit23   33 May  7  2020 bandit23
-r--------  1 bandit24 bandit24   33 May  7  2020 bandit24
-r--------  1 bandit25 bandit25   33 May  7  2020 bandit25
-r--------  1 bandit26 bandit26   33 May  7  2020 bandit26
-r--------  1 bandit27 bandit27   33 May  7  2020 bandit27
-r--------  1 bandit28 bandit28   33 May  7  2020 bandit28
-r--------  1 bandit29 bandit29   33 May  7  2020 bandit29
-r--------  1 bandit3  bandit3    33 May  7  2020 bandit3
-r--------  1 bandit30 bandit30   33 May  7  2020 bandit30
-r--------  1 bandit31 bandit31   33 May  7  2020 bandit31
-r--------  1 bandit32 bandit32   33 May  7  2020 bandit32
-r--------  1 bandit33 bandit33   33 May  7  2020 bandit33
-r--------  1 bandit4  bandit4    33 May  7  2020 bandit4
-r--------  1 bandit5  bandit5    33 May  7  2020 bandit5
-r--------  1 bandit6  bandit6    33 May  7  2020 bandit6
-r--------  1 bandit7  bandit7    33 May  7  2020 bandit7
-r--------  1 bandit8  bandit8    33 May  7  2020 bandit8
-r--------  1 bandit9  bandit9    33 May  7  2020 bandit9
bandit14@bandit:/etc/bandit_pass$ cat bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
bandit14@bandit:/etc/bandit_pass$


bandit14@bandit:/etc/bandit_pass$ nc localhost 30000
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr

bandit14@bandit:/etc/bandit_pass$
```
