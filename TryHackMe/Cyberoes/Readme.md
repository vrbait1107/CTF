## CyberHeroes

#### Want to be a part of the elite club of CyberHeroes? Prove your merit by finding a way to log in!

---

- **NAMP SCAN**

```

# Nmap 7.60 scan initiated Wed Oct  5 06:49:13 2022 as: nmap -sC -sV -oN nmap.txt 10.10.236.173
Nmap scan report for ip-10-10-236-173.eu-west-1.compute.internal (10.10.236.173)
Host is up (0.0012s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.4 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.48 ((Ubuntu))
|_http-server-header: Apache/2.4.48 (Ubuntu)
|_http-title: CyberHeros : Index
MAC Address: 02:A9:8A:B8:B9:15 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Oct  5 06:49:22 2022 -- 1 IP address (1 host up) scanned in 9.51 seconds

```

- **NIKTO Scan**

```

- Nikto v2.1.5/2.1.5
+ Target Host: ip-10-10-236-173.eu-west-1.compute.internal
+ Target Port: 80
+ GET /: Server leaks inodes via ETags, header found with file /, fields: 0x19a8 0x5d940fff601c0 
+ GET /: The anti-clickjacking X-Frame-Options header is not present.
+ OPTIONS /: Allowed HTTP Methods: POST, OPTIONS, HEAD, GET 
+ GET /login.html: /login.html: Admin login page/section found.

```

Lets Visit the Web server

![Websites](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Cyberheroes/Picture-1.png)

We can clear see the authentication logic return in javascript
Username is h3ck3rBoi

![Reverse](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Cyberheroes/Picture-2.png)

Password is Reverse of 54321@terceSrepuS which is SuperSecret@12345

![Authentication](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Cyberheroes/Picture-3.png)

Username: h3ck3rBoi
Password : SuperSecret@12345

We got the flag

![Flag](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Cyberheroes/Picture-4.png)

***Answer the questions below***

1. **Uncover the flag!**
- **flag{edb0be532c540b1a150c3a7e85d2466e}**

---
