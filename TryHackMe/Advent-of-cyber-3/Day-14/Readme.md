## [Day 14] Networking Dev(Insecure)Ops

### Story

McDev - the head of the dev team, sends an alarming email stating that they're unable to update the best festival company's external web application. Without this update, no one can view the Best Festival Company's plan. The dev team has been using a CI/CD server to automatically push out updates to the server but the CI/CD server has been compromised. Can you help them get their server back?

### Learning Objectives

1. Understanding the CI/CD concept
2. Overview of risks associated with CI/CD
3. Having a basic understanding of CI/CD exploitation vectors

### What is CI/CD?

CI/CD are two terms that will often come up when talking about software development and DevOps. Their definitions are pretty straightforward.
CI: Continuous Integration is the process in which software source code is kept in a central repository (such as GitHub). All changes are stored in this central repository to avoid ending up with different versions of the same code.
CD: Continuous Delivery is the following (sometimes integral) step of the continuous integration model where code is automatically deployed to the test, pre-production, or production environments. CD is sometimes used as an acronym for "Continuous Deployment". If you feel like the terms above don't seem to have clear limits, you are right. CI, CD, and the other CD are all part of DevOps best practices that aim to make code delivery faster and more reliable.

CI/CD should be considered as a set of practices that are put in place to enable development teams to make changes, test their code, and deploy the application more reliably.
We should think of CI/CD as a continuous process or loop that includes steps of the software development process.

### Risks Associated with CI/CD

The CI/CD integration approach seems to be an effective way to mitigate risks that may result from manually aggregating changes made to the code, manually testing them, and manually deploying the updated version of the application. However, some risks associated with the CI/CD process should be taken into consideration when dealing with such an integration. As a penetration tester, one of our goals would be to uncover weaknesses in the automation process. These can vary from file permissions to configuration errors made when installing any CI/CD automation software. DevOps teams typically use software such as Jenkins, GitLab, Bamboo, AWS CodePipeline, etc., to automate CI/CD steps summarized above.

Major risks related to a CI/CD integration are mentioned below:

- Access security: The increasing number of integration points can make access management difficult. Any component integrated with the process may need partial or full access to another component. In this case, allowing too much access can also open a path for malicious activity.
- Permissions: Components are connected with each other and perform their tasks with user accounts. Similar to access security, user permissions should be checked.
- Keys and secrets: Many integrations are done using keys (API keys, ID keys, etc.) or secrets. These should be secured. Otherwise, anyone could potentially access resources using this authentication method.
- User security: User accounts are another successful attack vector often used by cybercriminals. Any user who has access to the source code repository could include a malicious component in the codebase and could be included in the deployed application.
- Default configuration: Some platforms are known to have default credentials and vulnerabilities. If the default credentials are not changed, and in use within the CI/CD process, this could result in the complete compromise of the infrastructure.

### The Grinch CI/CD

The Grinch has put his own version of a CI/CD pipeline in place. He has used BASH scripts and scheduled jobs to automate the process. Let's dive in.

Visiting MACHINE_IP from your browser will show the Grinch is waiting for the loot, but not here.

At this stage, we can run a `dirb` scan to discover the MACHINE_IP/admin page, which looks more promising.

Looking at the source code, we see something interesting. There is an iFrame that refers to the `ls.html` page. This page seems suspiciously close to the output from running the `ls` command.

Connect to the target machine using in-browser access or via SSH with the credentials below:
username: mcskidy
password: Password1

Navigating to the `/home/thegrinch/scripts` folder and running the `ls` command will show that most of the scripts in the folder are not accessible by the McSkidy user.
The content of the `loot.sh` script gives us a clearer understanding of the ls.html file we have located earlier.

The code is simple; it runs the `ls` command and prints the output to the `ls.html` file. The Grinch can browse the page from anywhere within the network to see the loot he has accumulated.
Clever, this Grinch. However, there seems to be a problem regarding the permissions of his continuous integration attempt. McSkidy can change the contents of the `loot.sh` file.

Change the code in the file to print the contents of the `/etc/shadow` file. This will be conclusive proof that this permission misconfiguration not only creates a threat for the CI process but can also be used to escalate our privileges. If you are interested in learning more about privilege escalation techniques, please visit our Linux Privilege Escalation room.

This misconfiguration can be leveraged to read the contents of the Grinch's other scripts.
Let's have a look at the check.sh script using the vulnerability we have used to read the `/etc/shadow` file.

Within a couple of minutes, the `MACHINE_IP/admin` page will be updated to reveal the code of the check.sh script.

This script checks for the existence of a file named `remindme.txt` in the loot folder. If it finds the file, it prints the Grinch's password to an HTML file that will appear in MACHINE_IP/pass.html

Grinch's memory isn't what it used to be.

Alternatively, McSkidy could create a file named remindme.txt in the `/home/thegrinch/loot` folder and wait for the automation to work its magic.
Can you answer question 4 using this vector?

![Grinch](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-14/Picture-1.png "Grinch")

### Lessons Learned

This CI/CD simulation aimed to help showcase major types of vulnerabilities that are often seen in CI/CD automation. A locally installed Jenkins application can have an unpatched component deployed for various operational reasons. However, it is rare that a critical vulnerability remains unpatched for an extended period of time on infrastructure managed by a cloud service provider such as Amazon, Azure, or Google. This is the main reason you will more often see vulnerabilities being a result of improper access management, lax account privileges, or logic flaws.

In the example above, we have seen:

- **Folder permissions** that were too lax: The low privileged McSkidy user could write to the Grinch's "loot" folder.
- **File permissions** were misconfigured: The low privileged McSkidy user could change the contents of the loot.sh script.
- **Improper key protection:** In this example, Grinch's password can be seen as the secret key used to connect CI/CD components. If the key can be read from a configuration file, the attacker can reuse this key to their advantage.
- **Installation was not secure:** cronjobs were regularly running tasks without any controls for unauthorized changes. As you may have read in sector news, a similar lack of controls has led to the release of backdoored software.

---

**_Answer the questions below_**

1. **How many pages did the dirb scan find with its default wordlist?**

- **_Ans:- 4_**

```
root@ip-10-10-138-3:~# dirb http://10.10.251.12

-----------------
DIRB v2.22
By The Dark Raver
-----------------

START_TIME: Tue Dec 14 14:55:42 2021
URL_BASE: http://10.10.251.12/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt

-----------------

GENERATED WORDS: 4612

---- Scanning URL: http://10.10.251.12/ ----
+ http://10.10.251.12/admin (CODE:200|SIZE:363)
+ http://10.10.251.12/index.html (CODE:200|SIZE:169)
+ http://10.10.251.12/server-status (CODE:403|SIZE:277)
+ http://10.10.251.12/warez (CODE:200|SIZE:606)

-----------------
END_TIME: Tue Dec 14 14:56:36 2021
DOWNLOADED: 4612 - FOUND: 4
root@ip-10-10-138-3:~#

```

2. **How many scripts do you see in the /home/thegrinch/scripts folder?**

- **_Ans:- 4_**

![Scripts List](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-14/Picture-2.png "Scripts List")

3. **What are the five characters following $6$G in pepper's password hash?**

- **_Ans:- ZUP42_**

![Source Code](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-14/Picture-3.png "Source Code")

![Loot.sh](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-14/Picture-4.png "Loot.sh")

![Shadow File](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-14/Picture-5.png "Shadow File")

```
root:_:18561:0:99999:7::: daemon:_:18561:0:99999:7::: bin:_:18561:0:99999:7::: sys:_:18561:0:99999:7::: sync:_:18561:0:99999:7::: games:_:18561:0:99999:7::: man:_:18561:0:99999:7::: lp:_:18561:0:99999:7::: mail:_:18561:0:99999:7::: news:_:18561:0:99999:7::: uucp:_:18561:0:99999:7::: proxy:_:18561:0:99999:7::: www-data:_:18561:0:99999:7::: backup:_:18561:0:99999:7::: list:_:18561:0:99999:7::: irc:_:18561:0:99999:7::: gnats:_:18561:0:99999:7::: nobody:_:18561:0:99999:7::: systemd-network:_:18561:0:99999:7::: systemd-resolve:_:18561:0:99999:7::: syslog:_:18561:0:99999:7::: messagebus:_:18561:0:99999:7::: \_apt:_:18561:0:99999:7::: lxd:_:18561:0:99999:7::: uuidd:_:18561:0:99999:7::: dnsmasq:_:18561:0:99999:7::: landscape:_:18561:0:99999:7::: sshd:_:18561:0:99999:7::: pollinate:\*:18561:0:99999:7::: ubuntu:!:18942:0:99999:7::: thegrinch:$6$iiajscL7$7YgS0mCSs8ROHgS/4VP1itLix.T7onR26n4gdHFNAYnF/jVY7N4No11Yuy2RtLwXxJE3Vzl6zBdXXu5GUBJCj0:18942:0:99999:7::: mcskidy:$6$g81UcX1e$az/mXtNiOt9tMDb6lixDN3c1yH2GhcJVlAIWYB/WYNgujmxHafZdhD91ppxB.x7RIkH9DbpS6XQxe0piA2p2L1:18942:0:99999:7::: pepper:$6$GZUP42Y2$QYDESrTO9T517RDzR6cGXOANA/H4For7odahhn/DUdeWfEXtG9ZLHnZl4PLbfm8WF0GRB4ti9ij6w0NwBPunI/:18942:0:99999:7:::

```

4. **What is the content of the flag.txt file on the Grinch's user’s desktop?**

- **_Ans:- DI3H4rdIsTheBestX-masMovie!_**

![Loot.sh](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-14/Picture-6.png "Loot.sh")

![Flag.txt](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-14/Picture-7.png "Flag.txt")

---
