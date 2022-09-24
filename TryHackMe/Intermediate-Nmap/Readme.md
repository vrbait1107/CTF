## Intermediate Nmap

#### Can you combine your great nmap skills with other tools to log in to this machine?


You've learned some great nmap skills! Now can you combine that with other skills with netcat and protocols, to log in to this machine and find the flag? This VM MACHINE_IP is listening on a high port, and if you connect to it it may give you some information you can use to connect to a lower port commonly used for remote access!


1. First Scan machine with namp.

### NMAP

```
# Nmap 7.60 scan initiated Sat Sep 24 06:54:07 2022 as: nmap -sC -sV -oN nmap.txt 10.10.13.102
Nmap scan report for ip-10-10-13-102.eu-west-1.compute.internal (10.10.13.102)
Host is up (0.00088s latency).
Not shown: 997 closed ports
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.4 (Ubuntu Linux; protocol 2.0)
2222/tcp  open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.4 (Ubuntu Linux; protocol 2.0)
31337/tcp open  Elite?
| fingerprint-strings: 
|   DNSStatusRequest, DNSVersionBindReq, FourOhFourRequest, GenericLines, GetRequest, HTTPOptions, Help, Kerberos, LANDesk-RC, LDAPBindReq, LDAPSearchReq, LPDString, NCP, NULL, NotesRPC, RPCCheck, RTSPRequest, SIPOptions, SMBProgNeg, SSLSessionReq, TLSSessionReq, TerminalServer, X11Probe: 
|     In case I forget - user:pass
|_    ubuntu:Dafdas!!/str0ng
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port31337-TCP:V=7.60%I=7%D=9/24%Time=632E9B83%P=x86_64-pc-linux-gnu%r(N
SF:ULL,35,"In\x20case\x20I\x20forget\x20-\x20user:pass\nubuntu:Dafdas!!/st
SF:r0ng\n\n")%r(GetRequest,35,"In\x20case\x20I\x20forget\x20-\x20user:pass
SF:\nubuntu:Dafdas!!/str0ng\n\n")%r(SIPOptions,35,"In\x20case\x20I\x20forg
SF:et\x20-\x20user:pass\nubuntu:Dafdas!!/str0ng\n\n")%r(GenericLines,35,"I
SF:n\x20case\x20I\x20forget\x20-\x20user:pass\nubuntu:Dafdas!!/str0ng\n\n"
SF:)%r(HTTPOptions,35,"In\x20case\x20I\x20forget\x20-\x20user:pass\nubuntu
SF::Dafdas!!/str0ng\n\n")%r(RTSPRequest,35,"In\x20case\x20I\x20forget\x20-
SF:\x20user:pass\nubuntu:Dafdas!!/str0ng\n\n")%r(RPCCheck,35,"In\x20case\x
SF:20I\x20forget\x20-\x20user:pass\nubuntu:Dafdas!!/str0ng\n\n")%r(DNSVers
SF:ionBindReq,35,"In\x20case\x20I\x20forget\x20-\x20user:pass\nubuntu:Dafd
SF:as!!/str0ng\n\n")%r(DNSStatusRequest,35,"In\x20case\x20I\x20forget\x20-
SF:\x20user:pass\nubuntu:Dafdas!!/str0ng\n\n")%r(Help,35,"In\x20case\x20I\
SF:x20forget\x20-\x20user:pass\nubuntu:Dafdas!!/str0ng\n\n")%r(SSLSessionR
SF:eq,35,"In\x20case\x20I\x20forget\x20-\x20user:pass\nubuntu:Dafdas!!/str
SF:0ng\n\n")%r(TLSSessionReq,35,"In\x20case\x20I\x20forget\x20-\x20user:pa
SF:ss\nubuntu:Dafdas!!/str0ng\n\n")%r(Kerberos,35,"In\x20case\x20I\x20forg
SF:et\x20-\x20user:pass\nubuntu:Dafdas!!/str0ng\n\n")%r(SMBProgNeg,35,"In\
SF:x20case\x20I\x20forget\x20-\x20user:pass\nubuntu:Dafdas!!/str0ng\n\n")%
SF:r(X11Probe,35,"In\x20case\x20I\x20forget\x20-\x20user:pass\nubuntu:Dafd
SF:as!!/str0ng\n\n")%r(FourOhFourRequest,35,"In\x20case\x20I\x20forget\x20
SF:-\x20user:pass\nubuntu:Dafdas!!/str0ng\n\n")%r(LPDString,35,"In\x20case
SF:\x20I\x20forget\x20-\x20user:pass\nubuntu:Dafdas!!/str0ng\n\n")%r(LDAPS
SF:earchReq,35,"In\x20case\x20I\x20forget\x20-\x20user:pass\nubuntu:Dafdas
SF:!!/str0ng\n\n")%r(LDAPBindReq,35,"In\x20case\x20I\x20forget\x20-\x20use
SF:r:pass\nubuntu:Dafdas!!/str0ng\n\n")%r(LANDesk-RC,35,"In\x20case\x20I\x
SF:20forget\x20-\x20user:pass\nubuntu:Dafdas!!/str0ng\n\n")%r(TerminalServ
SF:er,35,"In\x20case\x20I\x20forget\x20-\x20user:pass\nubuntu:Dafdas!!/str
SF:0ng\n\n")%r(NCP,35,"In\x20case\x20I\x20forget\x20-\x20user:pass\nubuntu
SF::Dafdas!!/str0ng\n\n")%r(NotesRPC,35,"In\x20case\x20I\x20forget\x20-\x2
SF:0user:pass\nubuntu:Dafdas!!/str0ng\n\n");
MAC Address: 02:78:25:FF:5B:C3 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Sep 24 06:54:11 2022 -- 1 IP address (1 host up) scanned in 4.16 seconds

```

2. We have found there is 3 ports open and with fingerprint we found ssh username and password, lets login with ssh

```
root@ip-10-10-72-135:~/Desktop# ssh ubuntu@10.10.13.102 
The authenticity of host '10.10.13.102 (10.10.13.102)' can't be established.
ECDSA key fingerprint is SHA256:tD+Aiagv/4teueystsEl6q9ZNvNF9C8v+dsZj3fhbdQ.
Are you sure you want to continue connecting (yes/no)? 
Host key verification failed.
root@ip-10-10-72-135:~/Desktop# ssh ubuntu@10.10.13.102 
The authenticity of host '10.10.13.102 (10.10.13.102)' can't be established.
ECDSA key fingerprint is SHA256:tD+Aiagv/4teueystsEl6q9ZNvNF9C8v+dsZj3fhbdQ.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '10.10.13.102' (ECDSA) to the list of known hosts.
ubuntu@10.10.13.102's password: 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.13.0-1014-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.


ubuntu@f518fa10296d:/home$ ls -la
total 20
drwxr-xr-x 1 root   root   4096 Mar  2  2022 .
drwxr-xr-x 1 root   root   4096 Mar  2  2022 ..
drwxr-xr-x 1 ubuntu ubuntu 4096 Sep 24 05:57 ubuntu
drwxr-xr-x 2 root   root   4096 Mar  2  2022 user
ubuntu@f518fa10296d:/home$ cd ubuntu/
ubuntu@f518fa10296d:~$ ls
ubuntu@f518fa10296d:~$ ls -la
total 28
drwxr-xr-x 1 ubuntu ubuntu 4096 Sep 24 05:57 .
drwxr-xr-x 1 root   root   4096 Mar  2  2022 ..
-rw-r--r-- 1 ubuntu ubuntu  220 Feb 25  2020 .bash_logout
-rw-r--r-- 1 ubuntu ubuntu 3771 Feb 25  2020 .bashrc
drwx------ 2 ubuntu ubuntu 4096 Sep 24 05:57 .cache
-rw-r--r-- 1 ubuntu ubuntu  807 Feb 25  2020 .profile
ubuntu@f518fa10296d:~$ cd /home/user
ubuntu@f518fa10296d:/home/user$ ls
flag.txt
ubuntu@f518fa10296d:/home/user$ cat flag.txt 
flag{251f309497a18888dde5222761ea88e4}ubuntu@f518fa10296d:/home/user$

```



**_Answer the questions below_**

1. **Find the Flag**

- **_flag{251f309497a18888dde5222761ea88e4}ubuntu@f518fa10296d_**

---




