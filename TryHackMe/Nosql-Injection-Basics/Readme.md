## NoSQL injection Basics

#### A walkthrough depicting basic NoSQL injections on MongoDB.

### Task 1 Intro Introduction

Before we can learn about NoSQL injection, let's first take a look at what MongoDB is and how it works.

**MongoDB**

Much like MySQL, MariaDB, or PostgresSQL, MongoDB is another database where you can store data in an ordered way. MongoDB allows you to retrieve subsets of data in a quick and structured form. If you are familiar with relational databases, you can assume MongoDB works similarly to any other database. The major exception is that the information isn't stored on tables but rather in documents.

You can think of these documents as a simple dictionary structure where key-value pairs are stored. In a way, they are very similar to what you would call a record on a traditional relational database, but the information is just stored differently. For example, let's say we are creating a web application for the HR department, and we would like to store basic employee information. You would then create a document for each employee containing the data in a format that looks like this:

```
{"_id" : ObjectId("5f077332de2cdf808d26cd74")"username" : "lphillips", "first_name" : "Logan", "last_name" : "Phillips", "age" : "65", "email" : "lphillips@example.com" }

```

As you see, documents in MongoDB are stored in an associative array with an arbitrary number of fields.

MongoDB allows you to group multiple documents with a similar function together in higher hierarchy structures called collections for organizational purposes. Collections are the equivalent of tables in relational databases. Continuing with our HR example, all the employee's documents would be conveniently grouped in a collection called "people" as shown in the diagram below.

![Collections](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-1.png)

Multiple collections are finally grouped in databases, which is the highest hierarchical element in MongoDB. In relational databases, the database concept groups tables together. In MongoDB, it groups related collections.

![Database](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-2.png)

**Querying the database**

As with any database, a special language is used to retrieve information from the database. Just as relational databases use some variant of SQL, non-relational databases such as MongoDB use NoSQL. In general terms, NoSQL refers to any way of querying a database that is not SQL, meaning it may vary depending on the database used.

With MongoDB, queries use a structured associative array that contains groups of criteria to be met to filter the information. These filters offer similar functionality to a where clause in SQL and offer operators to build complex queries if needed.

To better understand NoSQL queries, let's start by assuming we have a database with a collection of people containing the following three documents:

![Database](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-3.png)

**_Answer the questions below_**

1. **Read the introduction.**

- **_No Answer Needed._**

---

### Task 2 NoSQL injection 

Note: Make sure to start your machine and navigate to http://MACHINE_IP to start the exercise.


**How to inject NoSQL**

When looking at how NoSQL filters are built, bypassing them to inject any payload might look impossible, as they rely on creating a structured array. Unlike SQL injection, where queries were normally built by simple string concatenation, NoSQL queries require nested associative arrays. From an attacker's point of view, this means that to inject NoSQL, one must be able to inject arrays into the application.

Luckily for us, many server-side programming languages allow passing array variables by using a special syntax on the query string of an HTTP Request. For the purpose of this example, let's focus on the following code written in PHP for a simple login page:

![No SQL Injection](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-4.png)

The web application is making a query to MongoDB, using the "myapp" database and "login" collection, requesting any document that passes the filter ['username'=>$user, 'password'=>$pass], where both $user and $pass are obtained directly from HTTP POST parameters

If somehow we could send an array to the $user and $pass variables with the following content:

`$user = ['$ne'=>'xxxx']`

`$pass = ['$ne'=>'yyyy']`

The resulting filter would end up looking like this:

`['username'=>['$ne'=>'xxxx'], 'password'=>['$ne'=>'yyyy']]`

We could trick the database into returning any document where the username isn't equal to 'xxxx,' and the password isn't equal to 'yyyy'. This would probably return all documents in the login collection. As a result, the application would assume a correct login was performed and let us into the application with the privileges of the user corresponding to the first document obtained from the database.

The problem that remains unsolved is how to pass an array as part of a POST HTTP Request. It turns out that PHP and many other languages allow you to pass an array by using the following notation on the POST Request Body:

`user[$ne]=xxxx&pass[$ne]=yyyy`

So let's fire up our favourite proxy and try to test this. For this guide we will be using Burp Proxy.

**_Answer the questions below_**

1. **Read the task's content.**

- **_No Answer Needed._**

---

### Task 3 Bypassing the Login Screen 

Bypassing the login screen

First of all, let's open the website on http://10.10.104.173/ and send an incorrect user/pass to capture the request on Burp:

![Login Screen](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-5.png)

The original captured login request looks like this:

![Burp Request](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-6.png)

We now proceed to intercept another login request and modify the user and pass variables to send the desired arrays:

![Modifued Burp Request](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-7.png)

This forces the database to return all user documents and as a result we are finally logged into the application:

![Flag](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-8.png)


![Original Flag](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-15.png)

**_Answer the questions below_**

1. **When bypassing the login screen using the $ne operator, which user are you logged in as? .**

- **_Admin_**

---

### Task 4 Logging in as Other Users 

**Logging in as other users**

We have managed to bypass the application's login screen, but with the former technique, we can only login as the first user returned by the database. By making use of the $nin operator, we are going to modify our payload so that we can control which user we want to obtain.

First, the $nin operator allows us to create a filter by specifying criteria where the desired documents have some field, not in a list of values. So if we would want to log in as any user except for the user admin, we could modify our payload to look like this:

![Burp Request](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-9.png)


This would translate to a filter that has the following structure:

`['username'=>['$nin'=>['admin'] ], 'password'=>['$ne'=>'aweasdf']]`

Which tells the database to return any user for whom the username isn't admin and the password isn't aweasdf. As a result, we are now granted access to another user's account.

Notice that the $nin operator receives a list of values to ignore. We can continue to expand the list by adjusting our payload as follows:

![Burp Request](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-10.png)

This would result in a filter like this:

`['username'=>['$nin'=>['admin', 'jude'] ], 'password'=>['$ne'=>'aweasdf']]`

This can be repeated as many times as needed until we gain access to all of the available accounts.

![Original Flag](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-16.png)

**_Answer the questions below_**

1. **How many users are there in total?  .**

- **_3_**

2. **There is a user that starts with the letter "p". What is his username??  .**

- **_pedro_**

---

### Task 5 Extracting Users' Passwords 

**Extracting users' passwords**

At this point, we have access to all of the accounts in the application. However, it is important to try to extract the actual passwords in use as they might be reused in other services. To accomplish this, we will be abusing the $regex operator to ask a series of questions to the server that allow us to recover the passwords via a process that resembles playing the game hangman.

First, let's take one of the users discovered before and try to guess the length of his password. We will be using the following payload to do that:

![Burp Request](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-11.png)

we are asking the database if there is a user with a username of admin and a password that matches the regex: ^.{7}$. This basically represents a wildcard word of length 7. Since the server responds with a login error, we know the password length for the user admin isn't 7. After some trial and error, we finally arrived at the correct answer:


![Burp Request](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-12.png)

We now know the password for user admin has length 5. Now to figure the actual content, we modify our payload as follows:

![Burp Request](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-13.png)

We are now working with a regex of length 5 (a single letter c plus 4 dots), matching the discovered password length, and asking if the admin's password matches the regex ^c....$ , which means it starts with a lowercase c, followed by any 4 characters. Since the server response is an invalid login, we now know the first letter of the password can't be "c". We continue iterating over all available characters until we get a successful response from the server:

![Burp Request](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Nosql-Injection-Basics/Picture-14.png)

This confirms that the first letter of admin's password is 'a'. The same process can be repeated for the other letters until the full password is recovered. This can be repeated for other users as well if needed.



```
POST /login.php HTTP/1.1
Host: 10.10.68.12
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 32
Origin: http://10.10.68.12
DNT: 1
Connection: close
Referer: http://10.10.68.12/
Upgrade-Insecure-Requests: 1
Sec-GPC: 1

user=admin&pass=test&remember=on

```

Find Length of John Using Intruder Fuzz the number.


```
POST /login.php HTTP/1.1
Host: 10.10.68.12
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 32
Origin: http://10.10.68.12
DNT: 1
Connection: close
Referer: http://10.10.68.12/
Upgrade-Insecure-Requests: 1
Sec-GPC: 1

user=admin&pass[$regex]=^.{0}$&remember=on

```
then find out password

```
POST /login.php HTTP/1.1
Host: 10.10.68.12
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.93 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 32
Origin: http://10.10.68.12
DNT: 1
Connection: close
Referer: http://10.10.68.12/
Upgrade-Insecure-Requests: 1
Sec-GPC: 1

user=admin&pass[$regex]=^1.......$&remember=on

```

```

$ ssh pedro@10.10.68.12
pedro@10.10.68.12's password:
Permission denied, please try again.
pedro@10.10.68.12's password:
Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 4.15.0-147-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
Last login: Wed Jun 23 03:34:24 2021 from 192.168.100.250
pedro@nosql-nolife:~$ ls -la
total 32
drwxr-xr-x 3 pedro pedro 4096 Jun 23 03:38 .
drwxr-xr-x 4 root  root  4096 Jun 23 03:33 ..
lrwxrwxrwx 1 pedro pedro    9 Jun 23 03:38 .bash_history -> /dev/null
-rw-r--r-- 1 pedro pedro  220 Jun 23 03:33 .bash_logout
-rw-r--r-- 1 pedro pedro 3771 Jun 23 03:33 .bashrc
drwx------ 2 pedro pedro 4096 Jun 23 03:34 .cache
-rw-rw-r-- 1 pedro pedro   20 Jun 23 03:35 flag.txt
-rw-r--r-- 1 pedro pedro  807 Jun 23 03:33 .profile
-rw------- 1 pedro pedro  734 Jun 23 03:35 .viminfo
pedro@nosql-nolife:~$ cat flag.txt
flag{N0Sql_n01iF3!}
pedro@nosql-nolife:~$

```

**_Answer the questions below_**

1. **What is john's password?.**

- **_10584312_**

2. **One of the users seems to be reusing his password for many services. Find which one and connect through SSH to retrieve the final flag!**

- ***flag{N0Sql_n01iF3!}***

---


