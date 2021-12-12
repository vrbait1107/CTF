## [Day 11] Networking Where Are The Reindeers?

Before we begin, we suggest that you start the attached Machine and the AttackBox as you will need to use these resources to answer the questions at the end.

McDatabaseAdmin came rushing into the room and cried to McSkidy, “We’ve been locked out of the reindeer schedule - how will Santa’s transportation work for Christmas?” The grinch has locked McDatabaseAdmin of his system. You need to probe the external surface of the server to see if you get him his access back.

MS SQL Server is a Relational Database Management System (RDBMS). One simple way to think of a relational database is a group of tables that have relations. To gain a rough understanding of relational databases work, consider a shop's database with the following three tables:

1. Electronic Items
2. Customers
3. Invoices

Each item in the Electronic Items table has:

- ID
- Name
- Price
- Quantity

Each item in the Customers table has its own attributes as well:

- ID
- Name
- Email
- Phone

Finally, the Invoices table will refer to a customer and one or more electronic items. The Invoice table will refer to an “entity” from another table using its ID. This way, we only need to have the customer details and electronic item details written once instead of copying them to each new invoice. This case is a simplified example of a relational database. The figure below shows how the three tables are related.

![Database](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-11/Picture-1.png "Database")

The transportation schedule is in the reindeer database. However, McDatabaseAdmin can no longer log in to his system after the grinch changed the system password. Let’s see how we can help. Make sure you have started the attached Machine along with the AttackBox. Give them a few minutes to fully start before proceeding to answer the following questions.

![Grinch](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-11/Picture-2.png "Grinch")

---

**_Answer the questions below_**

1. **You decided that the first step would be to check the running services on `10.10.54.175`. You resort to yesterday’s tool, Nmap.**

**Knowing that `10.10.54.175` is a MS Windows system, you expect it to not respond to ping probes by default; therefore, you need to add -Pn to your nmap command to perform the scan. This instructs Nmap to skip pinging the target to see if the host is reachable. Without this option, Nmap will assume the target host is offline and not proceed with scanning.**

**1. There is an open port related to MS SQL Server accessible over the network. What is the port number?**

- **_Ans:- 1433_**

```
# Nmap 7.60 scan initiated Sun Dec 12 14:14:54 2021 as: nmap -sC -sV -Pn -oN /root/Desktop/nmap.txt 10.10.54.175
Nmap scan report for ip-10-10-54-175.eu-west-1.compute.internal (10.10.54.175)
Host is up (0.0015s latency).
Not shown: 996 filtered ports
PORT     STATE SERVICE       VERSION
22/tcp   open  ssh           OpenSSH for_Windows_7.7 (protocol 2.0)
| ssh-hostkey:
|   2048 2b:c5:31:04:b7:92:68:57:ac:3b:92:18:42:7b:c9:01 (RSA)
|   256 6c:ad:62:67:ad:1b:24:5d:d5:75:e1:07:1a:9a:69:29 (ECDSA)
|_  256 19:2f:29:26:a3:fb:37:21:4a:7b:7a:7b:de:e0:4f:12 (EdDSA)
135/tcp  open  msrpc         Microsoft Windows RPC
1433/tcp open  ms-sql-s      Microsoft SQL Server  15.00.2000.00
| ms-sql-ntlm-info:
|   Target_Name: AOC2021-MSSQL
|   NetBIOS_Domain_Name: AOC2021-MSSQL
|   NetBIOS_Computer_Name: AOC2021-MSSQL
|   DNS_Domain_Name: AOC2021-MSSQL
|   DNS_Computer_Name: AOC2021-MSSQL
|_  Product_Version: 10.0.17763
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2021-12-12T13:55:15
|_Not valid after:  2051-12-12T13:55:15
|_ssl-date: 2021-12-12T14:15:11+00:00; 0s from scanner time.
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| ssl-cert: Subject: commonName=AOC2021-MSSQL
| Not valid before: 2021-10-31T21:09:16
|_Not valid after:  2022-05-02T21:09:16
|_ssl-date: 2021-12-12T14:15:11+00:00; 0s from scanner time.
MAC Address: 02:B7:BA:07:46:C9 (Unknown)
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| ms-sql-info:
|   10.10.54.175:1433:
|     Version:
|       name: Microsoft SQL Server
|       number: 15.00.2000.00
|       Product: Microsoft SQL Server
|_    TCP port: 1433

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sun Dec 12 14:15:16 2021 -- 1 IP address (1 host up) scanned in 22.39 seconds

```

2. **Knowing the MS SQL Server is running and accessible over the network, we want to check if our username and password are still valid. Using the AttackBox terminal, we will use the command sqsh (pronounced skwish), an interactive database shell.**

**A simple syntax would be sqsh -S server -U username -P password, where:**

- **`S server` is used to specify the server, for example `-S 10.10.54.175`**
- **`U username` is used to provide the username; for example, `-U sa` is the username that we have enabled.**
- **`P password` lets us specify the password.**

**Let’s try to run, `sqsh -S 10.10.54.175 -U sa -P t7uLKzddQzVjVFJp`**

**If the connection is successful, you will get a prompt. What is the prompt that you have received?**

- **_Ans:- 1>_**

```
root@ip-10-10-6-3:~# sqsh -S 10.10.54.175 -U sa -P t7uLKzddQzVjVFJp
sqsh-2.1.7 Copyright (C) 1995-2001 Scott C. Gray
Portions Copyright (C) 2004-2010 Michael Peppler
This is free software with ABSOLUTELY NO WARRANTY
For more information type '\warranty'
1>

```

McDatabaseAdmin told us the database name is reindeer and it has three tables:

1. `names`
2. `presents`
3. `schedule`

To display the table names, you could use the following syntax, `SELECT * FROM table_name WHERE condition.`

- `SELECT` _ is used to return specific columns (attributes). _ refers to all the columns.
- `FROM table_name` to specify the table you want to read from.
- `WHERE condition` to specify the rows (entities).

In the terminal below, we executed the query, `SELECT * FROM reindeer.dbo.names;`. This SQL query should dump all the contents of the table names from the database reindeer. Note that the ; indicates the end of the SQL query, while go sends a SQL batch to the database.

```

pentester@TryHackMe$ sqsh -S 10.10.54.175 -U sa -P "t7uLKzddQzVjVFJp"
1> SELECT * FROM reindeer.dbo.names;
2> go
 id          first                                    last                                     nickname
 ----------- ---------------------------------------- ---------------------------------------- ----------------------------------------
           1 Dasher                                   Dasher                                   Dasher
           2 Dancer                                   Dancer                                   Dancer
           3 Prancer                                  Prancer                                  Prancer
           4 Vixen                                    Vixen                                    Vixen
           5 Comet                                    Comet                                    Comet
           6 Cupid                                    Cupid                                    Cupid
           7 Donner                                   Donder                                   Dunder
           8 Blitzen                                  Blixem                                   Blitzen
           9 Rudolph                                  Reindeer                                 Red Nosed

 (9 rows affected)

```

**We can see four columns in the table displayed above: id, first (name), last (name), and nickname. What is the first name of the reindeer of id 9?**

- **_Ans:- Rudolph_**

```
1> SELECT * FROM reindeer.dbo.names;
2> go
 id          first
	last
	nickname
 ----------- ----------------------------------------
	----------------------------------------
	----------------------------------------
           1 Dasher
	Dasher
	Dasher
           2 Dancer
	Dancer
	Dancer
           3 Prancer
	Prancer
	Prancer
           4 Vixen
	Vixen
	Vixen
           5 Comet
	Comet
	Comet
           6 Cupid
	Cupid
	Cupid
           7 Donner
	Donder
	Dunder
           8 Blitzen
	Blixem
	Blitzen
           9 Rudolph
	Reindeer
	Red Nosed

(9 rows affected)

```

**Check the table `schedule`. What is the destination of the trip scheduled on December 7?**

- **_Ans:- Prague_**

```
1> USE reindeer
2> go
1> SELECT * FROM schedule;
2> go

	id

	date                destination                                                                      notes

	----------------------------------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------------
	------------------- -------------------------------------------------------------------------------- ----------------------------------------

	2000

	Dec  5 2021 12:00am Tokyo                                                                            NULL

	2001

	Dec  3 2021 12:00am London                                                                           NULL

	2002

	Dec  1 2021 12:00am New York                                                                         NULL

	2003

	Dec  2 2021 12:00am Paris                                                                            NULL

	2004

	Dec  4 2021 12:00am California                                                                       NULL

	2005

	Dec  7 2021 12:00am Prague                                                                           NULL

	2006

	Dec 11 2021 12:00am Bangkok                                                                          NULL

	2007

	Dec 10 2021 12:00am Seoul                                                                            NULL

(8 rows affected)

```

**Check the table `presents`. What is the quantity available for the present “Power Bank”?**

- **_Ans:- 25000_**

```
3> SELECT * FROM presents;
4> go
 id          name                                                                             quantity
 ----------- -------------------------------------------------------------------------------- -----------
         100 Blanket                                                                                  500
         101 Laptop                                                                                  1000
         102 Cooler                                                                                   250
         103 BT Speaker                                                                              1000
         104 THM Subscription                                                                      100000
         105 Alarm Clock                                                                              500
         106 Cookies                                                                                10000
         107 THM T-Shirt                                                                           100000
         108 Power Bank                                                                             25000
         109 USB Hub                                                                                15000

(10 rows affected)
1>

```

**You have done fantastic work! You have helped McDatabaseAdmin retrieve the schedule! Now, let’s see if we can run MS Windows commands while interacting with the database. Some MS SQL Servers have `xp_cmdshell `enabled. If this is the case, we might have access to something similar to a command prompt.**

**The command syntax is `xp_cmdshell 'COMMAND'`;. Let’s try a simple command, whoami, which shows the user running the commands. In the terminal output below, after connecting to MS SQL Server, we tried xp_cmdshell 'whoami';, and we can see that the user is nt service\mssqlserver. This means that any command we pass to xp_cmdshell will run as nt service\mssqlserver.**

```
pentester@TryHackMe$ sqsh -S 10.10.54.175 -U sa -P "t7uLKzddQzVjVFJp"
1> xp_cmdshell 'whoami';
2> go

	output

[...]

	nt service\mssqlserver

	NULL

(2 rows affected, return status = 0)

```

**We can run other commands that we can execute on the MS Windows command line. For example, we can use dir to list files and directories and type filename to display the contents of a file. Consider the example in the terminal window below where we reveal the contents of the text file WindowsUpdate.log.**

```

pentester@TryHackMe$ sqsh -S 10.10.54.175 -U sa -P "t7uLKzddQzVjVFJp"
sqsh-2.5.16.1 Copyright (C) 1995-2001 Scott C. Gray
Portions Copyright (C) 2004-2014 Michael Peppler and Martin Wesdorp
This is free software with ABSOLUTELY NO WARRANTY
For more information type '\warranty'
1> xp_cmdshell 'type c:\windows\WindowsUpdate.log';
2> go

	output

[...]

        Windows Update logs are now generated using ETW (Event Tracing for Windows).
	Please run the Get-WindowsUpdateLog PowerShell command to convert ETW traces into a readable WindowsUpdate.log.

	NULL

	NULL

	For more information, please visit https://go.microsoft.com/fwlink/?LinkId=518345
(5 rows affected, return status = 0)
1>

```

**There is a flag hidden in the grinch user's home directory. What are its contents?**

- **_THM{YjtKeUy2qT3v5dDH}_**

```
1> xp_cmdshell 'type C:\Users\grinch\Documents\flag.txt'
2> go

	output




	----------------------------------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------

	THM{YjtKeUy2qT3v5dDH}




(1 row affected, return status = 0)
1>

```

**Congratulations, the flag you have recovered contains the password of McDatabaseAdmin! In this task, we learned how to use sqsh to interact with a MS SQL Server. We learned that if `xp_cmdshell` is enabled, we can execute system commands and read the output using sqsh.**

- **_No Answer Needed_**

---
