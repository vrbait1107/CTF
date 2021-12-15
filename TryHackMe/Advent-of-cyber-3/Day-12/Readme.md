## [Day 12] Networking Sharing Without Caring

### Story

Before we begin, we suggest that you start the attached Machine and the AttackBox as you will need to use these resources to answer the questions at the end.

Grinch Enterprises has been leaving traces of how their hackers have been accessing data from the system - you’ve found a unique server they use. We need your help to find out what method they’ve been using to extract any data.

We have noticed that MACHINE_IP is generating unusual traffic. We highly suspect that Grinch Enterprises are using it to access our data. We will use Nmap to discover the services are running on their server.

![Grinch](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-12/Picture-1.png "Grinch")

---

**_Answer the questions below_**

1. **Scan the target server with the IP `10.10.127.2`. Remember that MS Windows hosts block pings by default, so we need to add `-Pn`, for example, `nmap -Pn 10.10.127.2` for the scan to work correctly. How many TCP ports are open?**

- **_Ans:- 7_**

```
# Nmap 7.60 scan initiated Wed Dec 15 16:33:25 2021 as: nmap -Pn -oN Desktop/nmap.txt 10.10.127.2
Nmap scan report for ip-10-10-127-2.eu-west-1.compute.internal (10.10.127.2)
Host is up (0.00090s latency).
Not shown: 993 filtered ports
PORT     STATE SERVICE
22/tcp   open  ssh
111/tcp  open  rpcbind
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
2049/tcp open  nfs
3389/tcp open  ms-wbt-server
MAC Address: 02:32:86:19:E8:CB (Unknown)

# Nmap done at Wed Dec 15 16:33:54 2021 -- 1 IP address (1 host up) scanned in 29.66 seconds

```

**2. File System (NFS) is a protocol that allows the ability to transfer files between different computers and is available on many systems, including MS Windows and Linux. Consequently, NFS makes it easy to share files between various operating systems.**

**In the scan results you received earlier, you should be able to spot NFS or mountd, depending on whether you used the `-sV` option with Nmap or not. Which port is detected by Nmap as NFS or using the mountd service?**

- **_Ans:- 2049_**

**Now that we have discovered an NFS service is listening, let’s check what files are being shared. We can do this using the command `showmount`. In the terminal below, we run `showmount -e 10.10.127.2.` The `-e` or `--exports` show the NFS server’s export list.**

```
pentester@TryHackMe$ showmount -e 10.10.127.2
Export list for 10.10.127.2:
/share        (everyone)
/my-notes     (noone)

```

**Now that we have discovered an NFS service is listening, let’s check what files are being shared. We can do this using the command showmount. In the terminal below, we run showmount -e 10.10.127.2. The -e or --exports show the NFS server’s export list.**

```
pentester@TryHackMe$ showmount -e 10.10.127.2
Export list for 10.10.127.2:
/share (everyone)
/my-notes (noone)

```

**As we can see in the terminal output above, we have two shares, `/share` and `/my-notes`. After you have started the attached machine, use the AttackBox terminal to discover the shares on `10.10.127.2.`**

**3. How many shares did you find?**

- **_Ans:- 4_**

**4. How many shares show “everyone”?**

- **_Ans:- 3_**

```
root@ip-10-10-241-206:~# showmount -e 10.10.127.2
Export list for 10.10.127.2:
/share        (everyone)
/admin-files  (everyone)
/my-notes     (noone)
/confidential (everyone)
root@ip-10-10-241-206:~#

```

Let’s try to mount the shares we have discovered. We can create a directory on the AttackBox using mkdir tmp1, where tmp1 is the directory’s name. Then we can use this directory we created to mount the public NFS share using: `mount 10.10.127.2:/my-notes tmp1`.

```
pentester@TryHackMe$ mount 10.10.127.2:/my-notes tmp1
mount.nfs: access denied by server while mounting 10.10.127.2:/my-notes

```

We can see that the mounting has failed. `my-notes` is not public and requires specific authentication mechanisms that we don’t have access to. Let’s try again with the other folder, share.

```
pentester@TryHackMe$ mount 10.10.127.2:/share tmp1
```

We didn’t get any error messages, so it was a success. Let’s go inside the share to see what’s inside it using `cd tmp1`, then `ls`.

```
pentester@TryHackMe$ ls
132-0.txt  2680-0.txt
```

There are two text files. We can open the file using any text editor such as `nano FILENAME` or something quicker such as `less FILENAME`.

5. **What is the title of file 2680-0.txt?**

- **_Ans:- Meditations_**

```
root@ip-10-10-241-206:~/tmp1# head 2680-0.txt
Title: Meditations

Author: Marcus Aurelius

Translator: Meric Casaubon

Release Date: June, 2001 [eBook #2680]
[Most recently updated: March 8, 2021]

Language: English

```

**6. It seems that Grinch Enterprises has forgotten their SSH keys on our system. One of the shares contains a private key used for SSH authentication (id_rsa). What is the name of the share?**

- **_Ans:- confidential_**

```
root@ip-10-10-241-206:~/tmp1# mkdir tmp2
root@ip-10-10-241-206:~/tmp1# showmount -e 10.10.127.2
Export list for 10.10.127.2:
/share        (everyone)
/admin-files  (everyone)
/my-notes     (noone)
/confidential (everyone)
root@ip-10-10-241-206:~/tmp1# mount 10.10.127.2:/confidential tmp2
root@ip-10-10-241-206:~/tmp1# cd tmp2/
root@ip-10-10-241-206:~/tmp1/tmp2# ls
ssh
root@ip-10-10-241-206:~/tmp1/tmp2#

```

**7. We can calculate the MD5 sum of a file using `md5sum FILENAME`. What is the MD5 sum of id_rsa?**

- **_Ans:- 3e2d315a38f377f304f5598dc2f044de_**

```
root@ip-10-10-241-206:~/tmp1/tmp2# cd ssh/
root@ip-10-10-241-206:~/tmp1/tmp2/ssh# ls -la
total 6
drwxr-xr-x 2 nobody 4294967294   64 Nov 10 08:28 .
drwxr-xr-x 2 nobody 4294967294   64 Nov 10 08:33 ..
-rwx------ 1 ubuntu ubuntu     2602 Nov 10 08:25 id_rsa
-rwxr--r-- 1 ubuntu ubuntu      570 Nov 10 08:25 id_rsa.pub
root@ip-10-10-241-206:~/tmp1/tmp2/ssh# md5sum id_rsa
3e2d315a38f377f304f5598dc2f044de  id_rsa
root@ip-10-10-241-206:~/tmp1/tmp2/ssh#

```

---
