# Juicy Details

#### A popular juice shop has been breached! Analyze the logs to see what had happened...

### Logs Files

- [Apache Web Server access log file](https://github.com/vrbait1107/ctf_writeups/blob/main/tryhackme/assets/Juicy-Details/access.log)
- [Linux Authentication log file](https://github.com/vrbait1107/ctf_writeups/blob/main/tryhackme/assets/Juicy-Details/auth.log)
- [FTP Server log file](https://github.com/vrbait1107/ctf_writeups/blob/main/tryhackme/assets/Juicy-Details/vsftpd.log)


---
---

### Task 1: Introduction

You were hired as a SOC Analyst for one of the biggest Juice Shops in the world and an attacker has made their way into your network. 

Your tasks are:

- Figure out what techniques and tools the attacker used
- What endpoints were vulnerable
- What sensitive data was accessed and stolen from the environment

An IT team has sent you a zip file containing logs from the server. Download the attached file, type in "I am ready!" and get to work! There's no time to lose!

Answer the questions below

1. **Are you ready?**
- Ans I am Ready!

---
---

### Task 2 Reconnaissance 

Analyze the provided log files.

Look carefully at:

- What tools the attacker used
- What endpoints the attacker tried to exploit
- What endpoints were vulnerable


1. **What tools did the attacker use? (Order by the occurrence in the log)**
- Ans: Nmap, Hydra, sqlmap, curl, feroxbuster

---

2. **What endpoint was vulnerable to a brute-force attack?**
- Ans: /rest/user/login

```
::ffff:192.168.10.5 - - [11/Apr/2021:09:16:27 +0000] "GET /rest/user/login HTTP/1.0" 500 - "-" "Mozilla/5.0 (Hydra)"
::ffff:192.168.10.5 - - [11/Apr/2021:09:16:27 +0000] "GET /rest/user/login HTTP/1.0" 500 - "-" "Mozilla/5.0 (Hydra)"

```
---

3. **What endpoint was vulnerable to SQL injection?**
- Ans: /rest/products/search

```
::ffff:192.168.10.5 - - [11/Apr/2021:09:29:14 +0000] "GET /rest/products/search?q=1 HTTP/1.1" 200 - "-" "sqlmap/1.5.2#stable (http://sqlmap.org)"

```
---

4. **What parameter was used for the SQL injection?**
- Ans: q

```
::ffff:192.168.10.5 - - [11/Apr/2021:09:29:14 +0000] "GET /rest/products/search?q=1 HTTP/1.1" 200 - "-" "sqlmap/1.5.2#stable (http://sqlmap.org)"

```
---

5. **What endpoint did the attacker try to use to retrieve files? (Include the /)**
- Ans: /ftp

```
::ffff:192.168.10.5 - - [11/Apr/2021:09:34:33 +0000] "GET /ftp HTTP/1.1" 200 4852 "-" "feroxbuster/2.2.1"
::ffff:192.168.10.5 - - [11/Apr/2021:09:34:40 +0000] "GET /ftp/www-data.bak HTTP/1.1" 403 300 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0"
::ffff:192.168.10.5 - - [11/Apr/2021:09:34:43 +0000] "GET /ftp/coupons_2013.md.bak HTTP/1.1" 403 78965 "-" ""Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0"

```
---
---

### Task 3 Stolen data 

Analyze the provided log files.

Look carefully at:

- The attacker's movement on the website
- Response codes
- Abnormal query strings


1. **What section of the website did the attacker use to scrape user email addresses?**
- Ans: products reviews

```
::ffff:192.168.10.5 - - [11/Apr/2021:09:10:19 +0000] "GET /rest/products/41/reviews HTTP/1.1" 200 284 "http://192.168.10.4/" "Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0"

```
---

2. **Was their brute-force attack successful? If so, what is the timestamp of the successful login? (Yay/Nay, 11/Apr/2021:09:xx:xx +0000)**
- Ans: Yay, 11/Apr/2021:09:16:32 +0000

```
::ffff:192.168.10.5 - - [11/Apr/2021:09:16:32 +0000] "POST /rest/user/login HTTP/1.0" 401 26 "-" "Mozilla/5.0 (Hydra)"
::ffff:192.168.10.5 - - [11/Apr/2021:09:16:32 +0000] "POST /rest/user/login HTTP/1.0" 401 26 "-" "Mozilla/5.0 (Hydra)"

```
---

3. **What user information was the attacker able to retrieve from the endpoint vulnerable to SQL injection?**
- Ans: email, passwords

```
::ffff:192.168.10.5 - - [11/Apr/2021:09:31:04 +0000] "GET /rest/products/search?q=qwert%27))%20UNION%20SELECT%20id,%20email,%20password,%20%274%27,%20%275%27,%20%276%27,%20%277%27,%20%278%27,%20%279%27%20FROM%20Users-- HTTP/1.1" 200 - "-" "Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0"
::ffff:192.168.10.5 - - [11/Apr/2021:09:32:51 +0000] "GET /rest/products/search?q=qwert%27))%20UNION%20SELECT%20id,%20email,%20password,%20%274%27,%20%275%27,%20%276%27,%20%277%27,%20%278%27,%20%279%27%20FROM%20Users-- HTTP/1.1" 200 3742 "-" "curl/7.74.0"

```
---

4. **What files did they try to download from the vulnerable endpoint? (endpoint from the previous task, question #5)**
- Ans: coupons_2013.md.bak,www-data.bak

```
Sun Apr 11 09:35:45 2021 [pid 8154] [ftp] OK DOWNLOAD: Client "::ffff:192.168.10.5", "/www-data.bak", 2602 bytes, 544.81Kbyte/sec
Sun Apr 11 09:36:08 2021 [pid 8154] [ftp] OK DOWNLOAD: Client "::ffff:192.168.10.5", "/coupons_2013.md.bak", 131 bytes, 3.01Kbyte/sec

```
---

5. **What service and account name were used to retrieve files from the previous question? (service, username)**
- Ans: ftp,anonymous

```
Sun Apr 11 08:13:32 2021 [pid 6335] CONNECT: Client "::ffff:127.0.0.1"
Sun Apr 11 08:13:40 2021 [pid 6334] [anonymous] FAIL LOGIN: Client "::ffff:127.0.0.1"

```
---

6. What service and username were used to gain shell access to the server? (service, username)
- Ans: ssh,www-data

```
Apr 11 09:41:19 thunt sshd[8260]: Accepted password for www-data from 192.168.10.5 port 40112 ssh2

```
---
---










