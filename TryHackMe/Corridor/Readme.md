## Cooridor

#### Can you escape the Corridor?

### Task 1: Escape the Corridor

You have found yourself in a strange corridor. Can you find your way back to where you came?

In this challenge, you will explore potential IDOR vulnerabilities. Examine the URL endpoints you access as you navigate the website and note the hexadecimal values you find (they look an awful lot like a hash, don't they?). This could help you uncover website locations you were not expected to access.

***Answer the questions below***
- **flag{2477ef02448ad9156661ac40a6b8862e}**

---

**NMAP Scan**

```

# Nmap 7.60 scan initiated Mon Oct 10 04:48:37 2022 as: nmap -sC -sV -o nmap.txt 10.10.249.74
Nmap scan report for ip-10-10-249-74.eu-west-1.compute.internal (10.10.249.74)
Host is up (0.056s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Werkzeug httpd 2.0.3 (Python 3.10.2)
|_http-title: Corridor
MAC Address: 02:73:1B:04:EE:9B (Unknown)

Service detection performed.
 Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Oct 10 04:48:48 2022 -- 1 IP address (1 host up) scanned in 11.08 seconds

```

**NIKTO Scan**

```

- Nikto v2.1.5/2.1.5
+ Target Host: ip-10-10-249-74.eu-west-1.compute.internal
+ Target Port: 80
+ GET /: The anti-clickjacking X-Frame-Options header is not present.
+ OPTIONS /: Allowed HTTP Methods: GET, OPTIONS, HEAD 

```

**Web View**

We can see lots of doors.

![Index Page](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Corridor/Picture-1.png "Index Page")

Let's view view page source.

![View Page Source](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Corridor/Picture-2.png "View Page Source")

If we decoded url value then it is md5 values of 1,2,3 upto 13, so we flag would be at 0 or 14 md5 value, if we pass 0 md5 url then we got flag.

![Flag](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Corridor/Picture-3.png "Flag")


