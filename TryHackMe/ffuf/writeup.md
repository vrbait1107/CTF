# ffuf

<br/>

### Task 1: Introduction

```
1. I have ffuf installed
Ans: No Answer Needed

2. I have SecLists installed
Ans: No Answer Needed

```

<hr/>

### Task 2: Walkthrough Basics

```
1. What is the first file you found with a 200 status code?
Ans. favicon.ico

ffuf -u http://10.10.143.167/FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt

.htaccess               [Status: 403, Size: 289, Words: 21, Lines: 11]
.htpasswd               [Status: 403, Size: 289, Words: 21, Lines: 11]
config                  [Status: 301, Size: 314, Words: 20, Lines: 10]
docs                    [Status: 301, Size: 312, Words: 20, Lines: 10]
external                [Status: 301, Size: 316, Words: 20, Lines: 10]
favicon.ico             [Status: 200, Size: 1406, Words: 5, Lines: 2]
robots.txt              [Status: 200, Size: 26, Words: 3, Lines: 2]
server-status           [Status: 403, Size: 293, Words: 21, Lines: 11]

```

<hr/>

### Task 3: Walkthrough Finding pages and directories

```

1. What text file did you find?
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.143.167/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/SecLists/Discovery/Web-Content/raft-medium-files-lowercase.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
________________________________________________

favicon.ico             [Status: 200, Size: 1406, Words: 5, Lines: 2]
.htaccess               [Status: 403, Size: 289, Words: 21, Lines: 11]
robots.txt              [Status: 200, Size: 26, Words: 3, Lines: 2]
.                       [Status: 302, Size: 0, Words: 1, Lines: 1]
phpinfo.php             [Status: 302, Size: 0, Words: 1, Lines: 1]
php.ini                 [Status: 200, Size: 148, Words: 17, Lines: 5]
logout.php              [Status: 302, Size: 0, Words: 1, Lines: 1]
.html                   [Status: 403, Size: 285, Words: 21, Lines: 11]
about.php               [Status: 200, Size: 4840, Words: 331, Lines: 109]
.php                    [Status: 403, Size: 284, Words: 21, Lines: 11]
index.php               [Status: 302, Size: 0, Words: 1, Lines: 1]
login.php               [Status: 200, Size: 1523, Words: 89, Lines: 77]
setup.php               [Status: 200, Size: 4067, Words: 308, Lines: 123]
.htpasswd               [Status: 403, Size: 289, Words: 21, Lines: 11]
security.php            [Status: 302, Size: 0, Words: 1, Lines: 1]
.htm                    [Status: 403, Size: 284, Words: 21, Lines: 11]
.htpasswds              [Status: 403, Size: 290, Words: 21, Lines: 11]
.htgroup                [Status: 403, Size: 288, Words: 21, Lines: 11]
wp-forum.phps           [Status: 403, Size: 293, Words: 21, Lines: 11]
.htaccess.bak           [Status: 403, Size: 293, Words: 21, Lines: 11]
.htuser                 [Status: 403, Size: 287, Words: 21, Lines: 11]
.htc                    [Status: 403, Size: 284, Words: 21, Lines: 11]
.ht                     [Status: 403, Size: 283, Words: 21, Lines: 11]
:: Progress: [16243/16243] :: Job [1/1] :: 52 req/sec :: Duration: [0:00:04] :: Errors: 0 ::

2. What two file extensions were found for the index page?

Ans: php,phps
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.111.222/indexFUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/SecLists/Discovery/Web-Content/web-extensions.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
________________________________________________

.php                    [Status: 302, Size: 0, Words: 1, Lines: 1]
.phps                   [Status: 403, Size: 290, Words: 21, Lines: 11]
:: Progress: [39/39] :: Job [1/1] :: 25 req/sec :: Duration: [0:00:04] :: Errors: 0 ::


3. What page has a size of 4840?

Ans: about.php
________________________________________________

.php                    [Status: 403, Size: 284, Words: 21, Lines: 11]
.html                   [Status: 403, Size: 285, Words: 21, Lines: 11]
.html.php               [Status: 403, Size: 289, Words: 21, Lines: 11]
.htm                    [Status: 403, Size: 284, Words: 21, Lines: 11]
.htm.txt                [Status: 403, Size: 288, Words: 21, Lines: 11]
.htm.php                [Status: 403, Size: 288, Words: 21, Lines: 11]
logout.php              [Status: 302, Size: 0, Words: 1, Lines: 1]
config                  [Status: 301, Size: 314, Words: 20, Lines: 10]
docs                    [Status: 301, Size: 312, Words: 20, Lines: 10]
about.php               [Status: 200, Size: 4840, Words: 331, Lines: 109]
.                       [Status: 302, Size: 0, Words: 1, Lines: 1]
login.php               [Status: 200, Size: 1523, Words: 89, Lines: 77]
external                [Status: 301, Size: 316, Words: 20, Lines: 10]
.htaccess.txt           [Status: 403, Size: 293, Words: 21, Lines: 11]
.htaccess.php           [Status: 403, Size: 293, Words: 21, Lines: 11]
.htaccess               [Status: 403, Size: 289, Words: 21, Lines: 11]
.html.txt               [Status: 403, Size: 289, Words: 21, Lines: 11]
robots.txt              [Status: 200, Size: 26, Words: 3, Lines: 2]
setup.php               [Status: 200, Size: 4067, Words: 308, Lines: 123]
phpinfo.php             [Status: 302, Size: 0, Words: 1, Lines: 1]
security.php            [Status: 302, Size: 0, Words: 1, Lines: 1]
.php3                   [Status: 403, Size: 285, Words: 21, Lines: 11]
.phtml                  [Status: 403, Size: 286, Words: 21, Lines: 11]
index.php               [Status: 302, Size: 0, Words: 1, Lines: 1]
.htc.txt                [Status: 403, Size: 288, Words: 21, Lines: 11]
.htc.php                [Status: 403, Size: 288, Words: 21, Lines: 11]
.htc                    [Status: 403, Size: 284, Words: 21, Lines: 11]
instructions.php        [Status: 200, Size: 14014, Words: 1484, Lines: 263]
.php5                   [Status: 403, Size: 285, Words: 21, Lines: 11]
.html_var_de.php        [Status: 403, Size: 296, Words: 21, Lines: 11]
.html_var_de            [Status: 403, Size: 292, Words: 21, Lines: 11]
.html_var_de.txt        [Status: 403, Size: 296, Words: 21, Lines: 11]
.php4                   [Status: 403, Size: 285, Words: 21, Lines: 11]
server-status           [Status: 403, Size: 293, Words: 21, Lines: 11]
.htpasswd.php           [Status: 403, Size: 293, Words: 21, Lines: 11]
.htpasswd               [Status: 403, Size: 289, Words: 21, Lines: 11]
.htpasswd.txt           [Status: 403, Size: 293, Words: 21, Lines: 11]
.html.                  [Status: 403, Size: 286, Words: 21, Lines: 11]
.html..php              [Status: 403, Size: 290, Words: 21, Lines: 11]
.html..txt              [Status: 403, Size: 290, Words: 21, Lines: 11]
.html.html.txt          [Status: 403, Size: 294, Words: 21, Lines: 11]
.html.html              [Status: 403, Size: 290, Words: 21, Lines: 11]
.html.html.php          [Status: 403, Size: 294, Words: 21, Lines: 11]
.htpasswds.txt          [Status: 403, Size: 294, Words: 21, Lines: 11]
.htpasswds.php          [Status: 403, Size: 294, Words: 21, Lines: 11]
.htpasswds              [Status: 403, Size: 290, Words: 21, Lines: 11]
.htm..txt               [Status: 403, Size: 289, Words: 21, Lines: 11]
.htm..php               [Status: 403, Size: 289, Words: 21, Lines: 11]
.htm.                   [Status: 403, Size: 285, Words: 21, Lines: 11]
.htmll                  [Status: 403, Size: 286, Words: 21, Lines: 11]
.htmll.php              [Status: 403, Size: 290, Words: 21, Lines: 11]
.htmll.txt              [Status: 403, Size: 290, Words: 21, Lines: 11]
.phps                   [Status: 403, Size: 285, Words: 21, Lines: 11]
.html.old.txt           [Status: 403, Size: 293, Words: 21, Lines: 11]
.html.old               [Status: 403, Size: 289, Words: 21, Lines: 11]
.html.old.php           [Status: 403, Size: 293, Words: 21, Lines: 11]
.html.bak.txt           [Status: 403, Size: 293, Words: 21, Lines: 11]
.html.bak.php           [Status: 403, Size: 293, Words: 21, Lines: 11]
.ht.php                 [Status: 403, Size: 287, Words: 21, Lines: 11]
.ht                     [Status: 403, Size: 283, Words: 21, Lines: 11]
.html.bak               [Status: 403, Size: 289, Words: 21, Lines: 11]
.ht.txt                 [Status: 403, Size: 287, Words: 21, Lines: 11]
.htm.htm                [Status: 403, Size: 288, Words: 21, Lines: 11]
.htm.htm.txt            [Status: 403, Size: 292, Words: 21, Lines: 11]
.htm.htm.php            [Status: 403, Size: 292, Words: 21, Lines: 11]
.htgroup                [Status: 403, Size: 288, Words: 21, Lines: 11]
.hta                    [Status: 403, Size: 284, Words: 21, Lines: 11]
.hta.txt                [Status: 403, Size: 288, Words: 21, Lines: 11]
.html1                  [Status: 403, Size: 286, Words: 21, Lines: 11]
.hta.php                [Status: 403, Size: 288, Words: 21, Lines: 11]
.html1.php              [Status: 403, Size: 290, Words: 21, Lines: 11]
.htgroup.txt            [Status: 403, Size: 292, Words: 21, Lines: 11]
.htgroup.php            [Status: 403, Size: 292, Words: 21, Lines: 11]
.html1.txt              [Status: 403, Size: 290, Words: 21, Lines: 11]
.html.lck.txt           [Status: 403, Size: 293, Words: 21, Lines: 11]
.html.lck.php           [Status: 403, Size: 293, Words: 21, Lines: 11]
.html.lck               [Status: 403, Size: 289, Words: 21, Lines: 11]
.html.printable.txt     [Status: 403, Size: 299, Words: 21, Lines: 11]
.html.printable         [Status: 403, Size: 295, Words: 21, Lines: 11]
.html.printable.php     [Status: 403, Size: 299, Words: 21, Lines: 11]
.htm.lck                [Status: 403, Size: 288, Words: 21, Lines: 11]
.htm.lck.php            [Status: 403, Size: 292, Words: 21, Lines: 11]
.htm.lck.txt            [Status: 403, Size: 292, Words: 21, Lines: 11]
.htaccess.bak.txt       [Status: 403, Size: 297, Words: 21, Lines: 11]
.htmls.php              [Status: 403, Size: 290, Words: 21, Lines: 11]
.htaccess.bak.php       [Status: 403, Size: 297, Words: 21, Lines: 11]
.html.php               [Status: 403, Size: 289, Words: 21, Lines: 11]
.htmls                  [Status: 403, Size: 286, Words: 21, Lines: 11]
.html.php.php           [Status: 403, Size: 293, Words: 21, Lines: 11]
.htmls.txt              [Status: 403, Size: 290, Words: 21, Lines: 11]
.htaccess.bak           [Status: 403, Size: 293, Words: 21, Lines: 11]
.htx.php                [Status: 403, Size: 288, Words: 21, Lines: 11]
.htx.txt                [Status: 403, Size: 288, Words: 21, Lines: 11]
.html.php.txt           [Status: 403, Size: 293, Words: 21, Lines: 11]
.htx                    [Status: 403, Size: 284, Words: 21, Lines: 11]
.htlm.txt               [Status: 403, Size: 289, Words: 21, Lines: 11]
.htm2                   [Status: 403, Size: 285, Words: 21, Lines: 11]
.html-.txt              [Status: 403, Size: 290, Words: 21, Lines: 11]
.htlm.php               [Status: 403, Size: 289, Words: 21, Lines: 11]
.htm2.txt               [Status: 403, Size: 289, Words: 21, Lines: 11]
.html-                  [Status: 403, Size: 286, Words: 21, Lines: 11]
.htlm                   [Status: 403, Size: 285, Words: 21, Lines: 11]
.html-.php              [Status: 403, Size: 290, Words: 21, Lines: 11]
.htuser                 [Status: 403, Size: 287, Words: 21, Lines: 11]
.htuser.txt             [Status: 403, Size: 291, Words: 21, Lines: 11]
.htuser.php             [Status: 403, Size: 291, Words: 21, Lines: 11]
.htm2.php               [Status: 403, Size: 289, Words: 21, Lines: 11]
.htacess                [Status: 403, Size: 288, Words: 21, Lines: 11]
.htm.d.txt              [Status: 403, Size: 290, Words: 21, Lines: 11]
.htm.html.txt           [Status: 403, Size: 293, Words: 21, Lines: 11]
.htm.html               [Status: 403, Size: 289, Words: 21, Lines: 11]
.htm.old                [Status: 403, Size: 288, Words: 21, Lines: 11]
.htm.old.php            [Status: 403, Size: 292, Words: 21, Lines: 11]
.htm.html.php           [Status: 403, Size: 293, Words: 21, Lines: 11]
.html-1.php             [Status: 403, Size: 291, Words: 21, Lines: 11]
.html-1.txt             [Status: 403, Size: 291, Words: 21, Lines: 11]
.htm.old.txt            [Status: 403, Size: 292, Words: 21, Lines: 11]
.html.orig              [Status: 403, Size: 290, Words: 21, Lines: 11]
.html.orig.txt          [Status: 403, Size: 294, Words: 21, Lines: 11]
.html.orig.php          [Status: 403, Size: 294, Words: 21, Lines: 11]
.html.sav.php           [Status: 403, Size: 293, Words: 21, Lines: 11]
.html.sav               [Status: 403, Size: 289, Words: 21, Lines: 11]
.htm.d.php              [Status: 403, Size: 290, Words: 21, Lines: 11]
.html_.txt              [Status: 403, Size: 290, Words: 21, Lines: 11]
.html_files             [Status: 403, Size: 291, Words: 21, Lines: 11]
.html-1                 [Status: 403, Size: 287, Words: 21, Lines: 11]
.html.sav.txt           [Status: 403, Size: 293, Words: 21, Lines: 11]
.htacess.txt            [Status: 403, Size: 292, Words: 21, Lines: 11]
.htm.d                  [Status: 403, Size: 286, Words: 21, Lines: 11]
.hts.txt                [Status: 403, Size: 288, Words: 21, Lines: 11]
.html_.php              [Status: 403, Size: 290, Words: 21, Lines: 11]
.htmlpar.php            [Status: 403, Size: 292, Words: 21, Lines: 11]
.html_                  [Status: 403, Size: 286, Words: 21, Lines: 11]
.htmlpar                [Status: 403, Size: 288, Words: 21, Lines: 11]
.htmlpar.txt            [Status: 403, Size: 292, Words: 21, Lines: 11]
.htmlprint              [Status: 403, Size: 290, Words: 21, Lines: 11]
.html_files.php         [Status: 403, Size: 295, Words: 21, Lines: 11]
.hts                    [Status: 403, Size: 284, Words: 21, Lines: 11]
.html_files.txt         [Status: 403, Size: 295, Words: 21, Lines: 11]
.htacess.php            [Status: 403, Size: 292, Words: 21, Lines: 11]
.hts.php                [Status: 403, Size: 288, Words: 21, Lines: 11]
.htmlprint.txt          [Status: 403, Size: 294, Words: 21, Lines: 11]
.htmlprint.php          [Status: 403, Size: 294, Words: 21, Lines: 11]
:: Progress: [168879/168879] :: Job [1/1] :: 8384 req/sec :: Duration: [0:00:14] :: Errors: 0 ::


4. How many directories are there?

Ans: 4
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.111.222/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/SecLists/Discovery/Web-Content/raft-medium-directories-lowercase.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
________________________________________________

docs                    [Status: 301, Size: 312, Words: 20, Lines: 10]
config                  [Status: 301, Size: 314, Words: 20, Lines: 10]
external                [Status: 301, Size: 316, Words: 20, Lines: 10]
server-status           [Status: 403, Size: 293, Words: 21, Lines: 11]
                        [Status: 302, Size: 0, Words: 1, Lines: 1]
:: Progress: [26584/26584] :: Job [1/1] :: 273 req/sec :: Duration: [0:00:04] :: Errors: 2 ::

```

<hr/>

### Task 4: Walkthrough Using filters

```
1. After applying the fc filter, how many results were returned?
Ans: 11
______________________________________________

 :: Method           : GET
 :: URL              : http://10.10.111.222/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/SecLists/Discovery/Web-Content/raft-medium-files-lowercase.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
 :: Filter           : Response status: 403
________________________________________________

favicon.ico             [Status: 200, Size: 1406, Words: 5, Lines: 2]
logout.php              [Status: 302, Size: 0, Words: 1, Lines: 1]
robots.txt              [Status: 200, Size: 26, Words: 3, Lines: 2]
phpinfo.php             [Status: 302, Size: 0, Words: 1, Lines: 1]
.                       [Status: 302, Size: 0, Words: 1, Lines: 1]
php.ini                 [Status: 200, Size: 148, Words: 17, Lines: 5]
about.php               [Status: 200, Size: 4840, Words: 331, Lines: 109]
index.php               [Status: 302, Size: 0, Words: 1, Lines: 1]
setup.php               [Status: 200, Size: 4067, Words: 308, Lines: 123]
login.php               [Status: 200, Size: 1523, Words: 89, Lines: 77]
security.php            [Status: 302, Size: 0, Words: 1, Lines: 1]
:: Progress: [16243/16243] :: Job [1/1] :: 49 req/sec :: Duration: [0:00:04] :: Errors: 0 ::

2. After applying the mc filter, how many results were returned?
Ans: 6
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.111.222/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/SecLists/Discovery/Web-Content/raft-medium-files-lowercase.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200
________________________________________________

favicon.ico             [Status: 200, Size: 1406, Words: 5, Lines: 2]
robots.txt              [Status: 200, Size: 26, Words: 3, Lines: 2]
php.ini                 [Status: 200, Size: 148, Words: 17, Lines: 5]
about.php               [Status: 200, Size: 4840, Words: 331, Lines: 109]
setup.php               [Status: 200, Size: 4067, Words: 308, Lines: 123]
login.php               [Status: 200, Size: 1523, Words: 89, Lines: 77]
:: Progress: [16243/16243] :: Job [1/1] :: 284 req/sec :: Duration: [0:00:04] :: Errors: 0 ::


4. Which valuable file would have been hidden if you used -fc 403 instead of -fr?
Ans: wp-forum.phps
________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.111.222/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/SecLists/Discovery/Web-Content/raft-medium-files-lowercase.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
 :: Filter           : Regexp: /\..*
________________________________________________

favicon.ico             [Status: 200, Size: 1406, Words: 5, Lines: 2]
logout.php              [Status: 302, Size: 0, Words: 1, Lines: 1]
robots.txt              [Status: 200, Size: 26, Words: 3, Lines: 2]
phpinfo.php             [Status: 302, Size: 0, Words: 1, Lines: 1]
.                       [Status: 302, Size: 0, Words: 1, Lines: 1]
php.ini                 [Status: 200, Size: 148, Words: 17, Lines: 5]
about.php               [Status: 200, Size: 4840, Words: 331, Lines: 109]
index.php               [Status: 302, Size: 0, Words: 1, Lines: 1]
setup.php               [Status: 200, Size: 4067, Words: 308, Lines: 123]
security.php            [Status: 302, Size: 0, Words: 1, Lines: 1]
login.php               [Status: 200, Size: 1523, Words: 89, Lines: 77]
wp-forum.phps           [Status: 403, Size: 293, Words: 21, Lines: 11]
:: Progress: [16243/16243] :: Job [1/1] :: 86 req/sec :: Duration: [0:00:04] :: Errors: 0 ::

```

<hr/>

### Task 5: Walkthrough Fuzzing parameters

```
1. What is the parameter you found?
Ans: id
______________________________________________

 :: Method           : GET
 :: URL              : http://10.10.148.165/sqli-labs/Less-1/?FUZZ=1
 :: Wordlist         : FUZZ: /usr/share/wordlists/SecLists/Discovery/Web-Content/burp-parameter-names.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
 :: Filter           : Response words: 39
________________________________________________

id                      [Status: 200, Size: 721, Words: 37, Lines: 29]
:: Progress: [2588/2588] :: Job [1/1] :: 6017 req/sec :: Duration: [0:00:04] :: Errors: 0 ::

2. What is the highest valid id?
Ans: 14

________________________________________________

 :: Method           : GET
 :: URL              : http://10.10.148.165/sqli-labs/Less-1/?id=FUZZ
 :: Wordlist         : FUZZ: -
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
 :: Filter           : Response words: 33
________________________________________________

14                      [Status: 200, Size: 725, Words: 37, Lines: 29]
12                      [Status: 200, Size: 725, Words: 37, Lines: 29]
10                      [Status: 200, Size: 725, Words: 37, Lines: 29]
9                       [Status: 200, Size: 725, Words: 37, Lines: 29]
8                       [Status: 200, Size: 723, Words: 37, Lines: 29]
7                       [Status: 200, Size: 725, Words: 37, Lines: 29]
11                      [Status: 200, Size: 725, Words: 37, Lines: 29]
6                       [Status: 200, Size: 728, Words: 37, Lines: 29]
5                       [Status: 200, Size: 728, Words: 37, Lines: 29]
3                       [Status: 200, Size: 726, Words: 37, Lines: 29]
4                       [Status: 200, Size: 725, Words: 37, Lines: 29]
2                       [Status: 200, Size: 731, Words: 37, Lines: 29]
1                       [Status: 200, Size: 721, Words: 37, Lines: 29]
:: Progress: [256/256] :: Job [1/1] :: 13 req/sec :: Duration: [0:00:04] :: Errors: 0 ::


3. What is Dummy's password?
Ans: p@ssword

_______________________________________________

 :: Method           : POST
 :: URL              : http://10.10.148.165/sqli-labs/Less-11/
 :: Wordlist         : FUZZ: /usr/share/wordlists/SecLists/Passwords/Leaked-Databases/hak5.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : uname=Dummy&passwd=FUZZ&submit=Submit
 :: Output file      : ffuf.md
 :: File format      : md
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
 :: Filter           : Response size: 1435
________________________________________________

p@ssword                [Status: 200, Size: 1526, Words: 100, Lines: 50]
:: Progress: [2351/2351] :: Job [1/1] :: 5024 req/sec :: Duration: [0:00:05] :: Errors: 0 ::

```

### Task 6: Walkthrough Finding vhosts and subdomains

```
1. What is THMs private CDN subdomain?
Ans: assets.tryhackme.com

2. What is the private domain you can find with vhost enumeration but not with direct subdomain enumeration?
Ans: dev.google.com

```

### Task 7: Walkthrough Proxifying ffuf traffic

```
1. I understand how to make the traffic go through a proxy
Ans: No Answers Needed.

```

### Task 8 Questions Reviewing the options

```
Use this command ffuf -h

1. How do you save the output to a markdown file (ffuf.md)?
Ans: -of md -o ffuf.md

2. How do you re-use a raw http request file?
Ans: -request

3. How do you strip comments from a wordlist?
Ans: -ic

4. How would you read a wordlist from STDIN?
Ans: -w -

5. How do you print full URLs and redirect locations?
Ans: -v

6. What option would you use to follow redirects?
Ans: -r

7. How do you enable colorized output?
Ans: -c


```
