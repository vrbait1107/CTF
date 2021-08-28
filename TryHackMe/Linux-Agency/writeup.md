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
5. What is the mission5 flag?
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
8. What is the mission9 flag?
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
9. What is the mission10 flag?
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
10. What is the mission11 flag?
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
11. What is the mission12 flag?
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
12. What is the mission13 flag?
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
13. What is the mission14 flag?
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
14. What is the mission14 flag?
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
15. What is the mission14 flag?
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
