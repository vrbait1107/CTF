## Git Happens

#### Boss wanted me to create a prototype, so here it is! We even used something called "version control" that made deploying this really easy!

### NMAP SCAN

```
# Nmap 7.60 scan initiated Sat Jan 22 05:43:00 2022 as: nmap -sC -sV -oN nmap.txt 10.10.24.140
Nmap scan report for ip-10-10-24-140.eu-west-1.compute.internal (10.10.24.140)
Host is up (0.061s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    nginx 1.14.0 (Ubuntu)
| http-git:
|   10.10.24.140:80/.git/
|     Git repository found!
|_    Repository description: Unnamed repository; edit this file 'description' to name the...
|_http-server-header: nginx/1.14.0 (Ubuntu)
|_http-title: Super Awesome Site!
MAC Address: 02:28:2C:48:61:D5 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Jan 22 05:43:10 2022 -- 1 IP address (1 host up) scanned in 10.71 seconds

```

### GOBUSTER

```
/.git/HEAD (Status: 200)
/css (Status: 301)
/index.html (Status: 200)

```

### Robots.txt

No Robots.txt Found.

### Sitemap

No Sitemap Found.

### Exploitation

We have noticed that there is .git directory.
Let's Download with GitTools. [dumper.sh](https://github.com/internetwache/GitTools/blob/master/Dumper/gitdumper.sh)

USAGE `./dumper.sh http://Machine-IP/.git/ Destination Folder.`

```
root@ip-10-10-165-80:~/Desktop/git/.git# git log
commit d0b3578a628889f38c0affb1b75457146a4678e5 (HEAD -> master, tag: v1.0)
Author: Adam Bertrand <hydragyrum@gmail.com>
Date:   Thu Jul 23 22:22:16 2020 +0000

    Update .gitlab-ci.yml

commit 77aab78e2624ec9400f9ed3f43a6f0c942eeb82d
Author: Hydragyrum <hydragyrum@gmail.com>
Date:   Fri Jul 24 00:21:25 2020 +0200

    add gitlab-ci config to build docker file.

commit 2eb93ac3534155069a8ef59cb25b9c1971d5d199
Author: Hydragyrum <hydragyrum@gmail.com>
Date:   Fri Jul 24 00:08:38 2020 +0200

    setup dockerfile and setup defaults.

commit d6df4000639981d032f628af2b4d03b8eff31213
Author: Hydragyrum <hydragyrum@gmail.com>
Date:   Thu Jul 23 23:42:30 2020 +0200

    Make sure the css is standard-ish!

commit d954a99b96ff11c37a558a5d93ce52d0f3702a7d
Author: Hydragyrum <hydragyrum@gmail.com>
Date:   Thu Jul 23 23:41:12 2020 +0200

    re-obfuscating the code to be really secure!

commit bc8054d9d95854d278359a432b6d97c27e24061d
Author: Hydragyrum <hydragyrum@gmail.com>
Date:   Thu Jul 23 23:37:32 2020 +0200

    Security says obfuscation isn't enough.

    They want me to use something called 'SHA-512'

commit e56eaa8e29b589976f33d76bc58a0c4dfb9315b1
Author: Hydragyrum <hydragyrum@gmail.com>
Date:   Thu Jul 23 23:25:52 2020 +0200

    Obfuscated the source code.

    Hopefully security will be happy!

commit 395e087334d613d5e423cdf8f7be27196a360459
Author: Hydragyrum <hydragyrum@gmail.com>
Date:   Thu Jul 23 23:17:43 2020 +0200

    Made the login page, boss!

commit 2f423697bf81fe5956684f66fb6fc6596a1903cc
Author: Adam Bertrand <hydragyrum@gmail.com>
Date:   Mon Jul 20 20:46:28 2020 +0000

    Initial commit
root@ip-10-10-165-80:~/Desktop/git/.git#

```

Check for commit Made the Login Page.

Use Command `git show 395e087334d613d5e423cdf8f7be27196a360459`

We have found following Javscript Code.

```html
<script>
  +      function login() {
  +        let form = document.getElementById("login-form");
  +        console.log(form.elements);
  +        let username = form.elements["username"].value;
  +        let password = form.elements["password"].value;
  +        if (
  +          username === "admin" &&
  +          password === "Th1s_1s_4_L0ng_4nd_S3cur3_P4ssw0rd!"
  +        ) {
  +          document.cookie = "login=1";
  +          window.location.href = "/dashboard.html";
  +        } else {
  +          document.getElementById("error").innerHTML =
  +            "INVALID USERNAME OR PASSWORD!";
  +        }
  +      }
  +
</script>
```

---

**_Answer the questions below_**

1. **Find the Super Secret Password**

- **_Th1s_1s_4_L0ng_4nd_S3cur3_P4ssw0rd!_**

---
