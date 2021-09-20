## Wreath

#### Learn how to pivot through a network by compromising a public facing web machine and tunnelling your traffic to access other machines in Wreath's network. (Streak limitation only for non-subscribed users)

### Task 1 Intro Introduction

![Wreath Network](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Wreath/wreath-1.png)

Wreath is designed as a learning resource for beginners with a primary focus on:

- Pivoting
- Working with the Empire C2 (Command and Control) framework
- Simple Anti-Virus evasion techniques

The following topics will also be covered, albeit more briefly:

- Code Analysis (Python and PHP)
- Locating and modifying public exploits
- Simple webapp enumeration and exploitation
- Git Repository Analysis
- Simple Windows Post-Exploitation techniques
- CLI Firewall Administration (CentOS and Windows)
- Cross-Compilation techniques
- Coding wrapper programs
- Simple exfiltration techniques
- Formatting a pentest report

These will be taught in the course of exploiting the Wreath network.

This is designed as almost a sandbox environment to follow along with the teaching content; the focus will be on the above teaching points, rather than on initial access and privilege escalation exploits (contrary to other boxes on the platform where the focus is on the challenge).

**Tools:**
A zipfile containing the tools demonstrated throughout this room is attached to this task. That said, whilst these will work, it would be advisable to download the latest versions of the tools (as instructed by the tasks) during your progression through the content, rather than relying on the provided archive. The password for this zipfile is: `WreathNetwork.`

**Videos:**
[@DarkStar7471](https://twitter.com/DarkStar7471) has kindly created a series of videos to accompany the teaching content in the Wreath network. Please use these as your first line of support! Writeups in the form of pentest reports will also be made available.

The videos can be accessed directly from Dark's [YouTube channel](https://www.youtube.com/playlist?list=PLsqUCyw0Jf9sMYXly0uuwfKMu34roGNwk); however, each task in this room also contains a link to the relevant video.

Look for the "Play" button at the very bottom right of the screen:

This will update on a task-by-task basis so that it always points to the correct video.

**Prerequisites:**
This network is designed for beginners, but assumes basic competence in the [Linux command line](https://tryhackme.com/room/tryhackme.com/room/linuxfundamentalspart1) and fundamental hacking methodology. The ability to read and write a little code will also be useful. Any other required knowledge will be linked throughout the tasks. If you need help, please feel free to ask in the [TryHackMe Discord](https://discord.gg/tryhackme) -- there is a channel set up for this purpose in the help section there.

**Conduct:**
As this network is shared amongst a number of people, it goes without saying: please don't mess things up for others in the network. There are no password changes required in any of these tasks, and no files need deleted. At various stages in this network it will be necessary to upload files and tools to the remote box. Please upload these in the format: `toolname-username` (e.g. `socat-MuirlandOracle`, `shell-MuirlandOracle`.aspx, etc) to avoid overwriting work belonging to anyone else. In short, don't be a troll, be respectful, and have fun!

With that being said:- let's get started!

**_Answer the questions below_**

1. **Read the introduction.**

- **_No Answer Needed._**

---

### Task 2: Intro Accessing the Network

Before we get into the content, we need to know how to access the network.

Joining the network requires a 7 day streak or a subscription to TryHackMe. To limit the number of networks which have to stay active at any one point, network access will last for 10 days after joining, at which point you will be automatically be removed; however, rejoining does not require a streak so if you didn't manage to finish within the ten days, you are free to rejoin immediately and keep at it from where you left off. Progress will not be reset.

Whether you are using the AttackBox or a local machine to connect to the TryHackMe network, you will need to use OpenVPN with a connection pack specifically designed for this network.

If you are using a local machine then you will need to download a configuration pack from the [Access](https://tryhackme.com/access) page.

If you are a subscriber and are using the AttackBox then you will be able to find this connection pack in a directory on your desktop. This will be automatically connected when the AttackBox starts so **don't run the connection pack manually on the AttackBox if you are a subscriber.**

If you are not subscribed then you will need to download the connection pack as normal, copy and paste the contents into a file on the AttackBox, then connect as you would on a local VM.

Be aware that this is still a VPN (albeit with an automated startup sequence) on the AttackBox so you will need to use `ip a` to see your available IP addresses. Pick the one that starts with 10.50.x.x and use that for all reverse connections in the network.

**_Note:_** _You are encouraged to use your own VM when attacking the Wreath Network. The content in this room will be difficult to cover in the time available with a single AttackBox and the persistence of a local VM will be hugely advantageous. Equally, certain sections (such as the Empire section) will be very difficult to perform in the AttackBox. If you don't have a local Kali VM, pre-built versions can be found for VMware or VirtualBox; however, installing manually tends to be more reliable if you are comfortable doing so._

**_Answer the questions below_**

On the access page, click on the "Network" tab, then select "Wreath" from the dropdown menu:

![VPN](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Wreath/wreath-2.png)

**_Note:_** _this will only appear if you have joined the room. If you are only viewing the room just now, click the "Join" button at the top right of this page!_

1. **Click on the green download button on the access page and save the configuration pack somewhere on your local machine. If this does not work then you may have to click on the "Regenerate" button first, then give it ten seconds before attempting to download the pack.**

- **_No Answer Needed._**

Connecting to OpenVPN on Linux (using either Kali or the AttackBox) can be accomplished using the `openvpn` client.

To do this, from the same directory we saved the config in we use the command:
`sudo openvpn CONFIG_NAME.ovpn`

Obviously replacing the name of the config with the config that you downloaded. Wreath config packs follow a naming scheme of USERNAME-wreath.ovpn, so an example command might be:
`sudo openvpn MuirlandOracle-wreath.ovpn`

![VPN CONNECTION](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Wreath/wreath-3.png)

1. **This should give you access to the Wreath network!**

- **_No Answer Needed._**

2. **Without closing the connection, open a new terminal (Ctrl + T in most cases). This is the easiest way (technically speaking) to run the OpenVPN client in the background whilst still being able to use the CLI. If you are comfortable using a terminal multiplexer (e.g. Tmux) to create a connection in the background then doing so would be a more elegant solution.**

- **_No Answer Needed._**

**Controlling the Network:**

The network has three states: Running, Stopped, and Resetting.

The current state can be shown at the top right of the network box at the top of the page:

![Wreath Network Structure](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Wreath/wreath-4.png)

- Running means that the network is fully operational and can be connected to at will
- Stopped indicates that the network has gone to sleep. This happens when no one has pressed the "Extend" button within a set time limit so as to prevent the network from being constantly running with no one using it. It can be restarted by pressing the "Start" button. This does not reset the network back to a clean copy, so anything stored on the targets should still be there
- Resetting indicates that the network is currently in the process of being wiped clean and resetting back to its default state. This can be used when something (or someone) has happened to one of the targets rendering it broken

The three buttons below the network map can be used to control this functionality:

![Wreath Network Control Buttons](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Wreath/wreath-5.png)

- The "Start" button restarts the network once stopped
- The "Extend" button prevents the network from going to sleep. This button also contains a timer showing how long until the network shuts down
- The "Reset" button initiates a full wipe of the network. This requires a percentage of users in the network to click the button, thus preventing a single person from spamming resets

1. **Finally, the "Network Uptime" field at the bottom right of the network map indicates how long the network has been awake for. This is not necessarily the time since the last reset.**

- **_No Answer Needed._**

---

### Task 3: Intro Backstory

_Out of the blue, an old friend from university: Thomas Wreath, calls you after several years of no contact. You spend a few minutes catching up before he reveals the real reason he called:_

**_"So I heard you got into hacking? That's awesome! I have a few servers set up on my home network for my projects, I was wondering if you might like to assess them?"_**

_You take a moment to think about it, before deciding to accept the job -- it's for a friend after all._

_Turning down his offer of payment, you tell him:_

**_Answer the questions below_**

1. **I'll do it!**

- **_No Answer Needed._**

---

### Task 4: Intro Brief

Thomas has sent over the following information about the network:

_There are two machines on my home network that host projects and stuff I'm working on in my own time -- one of them has a webserver that's port forwarded, so that's your way in if you can find a vulnerability! It's serving a website that's pushed to my git server from my own PC for version control, then cloned to the public facing server. See if you can get into these! My own PC is also on that network, but I doubt you'll be able to get into that as it has protections turned on, doesn't run anything vulnerable, and can't be accessed by the public-facing section of the network. Well, I say PC -- it's technically a repurposed server because I had a spare license lying around, but same difference._

From this we can take away the following pieces of information:

- There are three machines on the network
- There is at least one public facing webserver
- There is a self-hosted git server somewhere on the network
- The git server is internal, so Thomas may have pushed sensitive information into it
- There is a PC running on the network that has antivirus installed, meaning we can hazard a guess that this is likely to be Windows
- By the sounds of it this is likely to be the server variant of Windows, which might work in our favour
  The (assumed) Windows PC cannot be accessed directly from the webserver

This is enough to get started!

**_Note:_** _You are also encouraged to treat this Network like a penetration test -- i.e. take notes and screenshots of every step and write a full report at the end (especially if you're not already familiar with writing such reports). Keeping track of any files (e.g. tools or payloads) and users you create would also be a good idea. Reports will not be marked, but the act of writing them is good practice for any professional work -- or certifications -- you may do in the future. There will be more information on the actual report writing in the `Debrief & Report` task, but for now just focus on extensive notes and screenshots. If you are not already comfortable taking notes, have a look into CherryTree or Notion as hierarchical notetaking applications and focus on documenting every step of the process. This room is written in a way that encourages easy note taking, so note down your kill-chain as you go along, and take lots of screenshots! Reports can be submitted to the room as writeups (in the format specified in the questions of the `Debrief & Report` task) -- the first five high-quality writeups submitted to the room are featured here!_

- [CheckN8](https://assets.tryhackme.com/additional/wreath-network/writeups/CheckN8%20-%20Wreath.pdf)
- [fil](https://assets.tryhackme.com/additional/wreath-network/writeups/lolKatz%20-%20Wreath.pdf)
- [SefD](https://assets.tryhackme.com/additional/wreath-network/writeups/SefD%20-%20Wreath.pdf)
- [M4t35Z](https://assets.tryhackme.com/additional/wreath-network/writeups/M4t35Z%20-%20Wreath.pdf)
- [IamNobody](https://assets.tryhackme.com/additional/wreath-network/writeups/IamNobody%20-%20Wreath.pdf)

**_Answer the questions below_**

1. **Let's go!**

- **_No Answer Needed._**

**Before we start, if you are using Kali, make sure that it's up to date:**
`sudo apt update && sudo apt upgrade`

2. **This should not be necessary on the AttackBox.**

- **_Ans: No Answer Needed._**

---

### Task 5: Webserver Enumeration

**As with any attack, we first begin with the enumeration phase. Completing the [Nmap](https://tryhackme.com/room/furthernmap) room (if you haven't already) will help with this section.**

**Thomas gave us an IP to work with (shown on the Network Panel at the top of the page). Let's start by performing a port scan on the first 15000 ports of this IP.**

**_Note:_** _Here (and in general), it's a good idea to save your scan results to a file so you don't have to re-run the same scan twice._

**_Answer the questions below_**

**NMAP SCAN**

```
# Nmap 7.91 scan initiated Mon Sep 20 21:40:16 2021 as: "C:\\Program Files\\Nmap\\nmap.exe" -sC -sV -p 1-15000 -oN nmap.txt 10.200.193.200
Nmap scan report for 10.200.193.200
Host is up (0.60s latency).
Not shown: 14995 filtered ports
PORT      STATE  SERVICE    VERSION
22/tcp    open   ssh        OpenSSH 8.0 (protocol 2.0)
| ssh-hostkey:
|   3072 9c:1b:d4:b4:05:4d:88:99:ce:09:1f:c1:15:6a:d4:7e (RSA)
|   256 93:55:b4:d9:8b:70:ae:8e:95:0d:c2:b6:d2:03:89:a4 (ECDSA)
|_  256 f0:61:5a:55:34:9b:b7:b8:3a:46:ca:7d:9f:dc:fa:12 (ED25519)
80/tcp    open   http       Apache httpd 2.4.37 ((centos) OpenSSL/1.1.1c)
|_http-server-header: Apache/2.4.37 (centos) OpenSSL/1.1.1c
|_http-title: Did not follow redirect to https://thomaswreath.thm
443/tcp   open   ssl/http   Apache httpd 2.4.37 ((centos) OpenSSL/1.1.1c)
| http-methods:
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.4.37 (centos) OpenSSL/1.1.1c
|_http-title: Thomas Wreath | Developer
| ssl-cert: Subject: commonName=thomaswreath.thm/organizationName=Thomas Wreath Development/stateOrProvinceName=East Riding Yorkshire/countryName=GB
| Not valid before: 2021-09-20T14:45:20
|_Not valid after:  2022-09-20T14:45:20
|_ssl-date: TLS randomness does not represent time
| tls-alpn:
|_  http/1.1
9090/tcp  closed zeus-admin
10000/tcp open   http       MiniServ 1.890 (Webmin httpd)
|_http-server-header: MiniServ/1.890
|_http-title: Login to Webmin
|_http-trane-info: Problem with XML parsing of /evox/about

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Sep 20 21:52:16 2021 -- 1 IP address (1 host up) scanned in 720.76 seconds

```

1. **How many of the first 15000 ports are open on the target?**

- **_4_**

2.  **Perform a service scan on these open ports.**
    **What OS does Nmap think is running?**

- **_centos_**

3. **Okay, we know what we're dealing with.**

**Open the IP in your browser -- what site does the server try to redirect you to?**

- **_https://thomaswreath.thm/_**

4. **You will have noticed that the site failed to resolve. Looks like Thomas forgot to set up the DNS!**

Add it to your hosts file manually. This can be accomplished by editing the `/etc/hosts` file on Linux/MacOS, or `C:\Windows\System32\drivers\etc\hosts` on Windows, to include the IP address, followed by a tab, then the domain name. Note: this must be done as root/Administrator.

It should look something like this when done, although the IP address and domain name will be different:
`10.10.10.10 example.thm`

```
10.200.193.200 https://thomaswreath.thm/


# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost

```

- **_No Answer Needed._**

5. Reload the webpage -- it should now resolve, but it will give you a different error related to the TLS certificate. This occurs because the box is not really connected to the internet and so cannot have a signed TLS certificate. In this instance it is safe to click "Advanced" -> "Accept Risk"; however, you should never do this in the real world.

In real life we would perform a "footprinting" phase of the engagement at this point. This essentially involves finding as much public information about the target as possible and noting it down. You never know what could prove useful!

**Read through the text on the page. What is Thomas' mobile phone number?**

- **_Ans:+447821548812_**

![Thomas Mobile Number](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Wreath/wreath-6.png)

6. **Let's have a look at the highest open port.**

**Look back at your service scan results: what server version does Nmap detect as running here?**

- **_MiniServ 1.890 (Webmin httpd)_**

7. **Put your answer to the last question into Google.**

**It appears that this service is vulnerable to an unauthenticated remote code execution exploit!**

**What is the CVE number for this exploit?**

- **_CVE-2019-15107_**

![Webmin Exploit](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Wreath/wreath-7.png)

8. **We have everything we need to break into this machine, so let's get going!**

- **_No Answer Needed_**
