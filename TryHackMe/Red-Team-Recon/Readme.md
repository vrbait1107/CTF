## Red Team Recon

#### Learn how to use DNS, advanced searching, Recon-ng, and Maltego to collect information about your target.

### Task 1: Introduction

“Know your enemy, know his sword.” wrote Miyamoto Musashi in his book, A Book of Five Rings: The Classic Guide to Strategy. He also wrote, “You win battles by knowing the enemy’s timing, and using a timing which the enemy does not expect.” Although this was written when swords and spears won battles, it also applies to cyberspace, where attacks are launched via keyboards and crafted packets. The more you know about your target’s infrastructure and personnel, the better you can orchestrate your attacks.

In a red team operation, you might start with no more than a company name, from which you need to start gathering information about the target. This is where reconnaissance comes into play. Reconnaissance (recon) can be defined as a preliminary survey or observation of your target (client) without alerting them to your activities. If your recon activities create too much noise, the other party would be alerted, which might decrease the likelihood of your success.

The tasks of this room cover the following topics:

- Types of reconnaissance activities
- WHOIS and DNS-based reconnaissance
- Advanced searching
- Searching by image
- Google Hacking
- Specialized search engines
- Recon-ng
- Maltego

![Reconnaissance](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Red-Team-Recon/Picture-1.jpg)

Some specific objectives we'll cover include:

- Discovering subdomains related to our target company
- Gathering publicly available information about a host and IP addresses
- Finding email addresses related to the target
- Discovering login credentials and leaked passwords
- Locating leaked documents and spreadsheets

Reconnaissance can be broken down into two parts — passive reconnaissance and active reconnaissance, as explained in Task 2. In this room, we will be focusing on passive reconnaissance, i.e., techniques that don’t alert the target or create 'noise'. In later rooms, we will use active reconnaissance tools that tend to be noisy by nature.

**_Answer the questions below_**

1. **We suggest you start the AttackBox and experiment with every command and tool we demonstrate.**

- **_No Answer Needed._**

---

### Task 2: Taxonomy of Reconnaissance

Reconnaissance (recon) can be classified into two parts:

1. Passive Recon: can be carried out by watching passively
2. Active Recon: requires interacting with the target to provoke it in order to observe its response.

Passive recon doesn't require interacting with the target. In other words, you aren't sending any packets or requests to the target or the systems your target owns. Instead, passive recon relies on publicly available information that is collected and maintained by a third party. Open Source Intelligence (OSINT) is used to collect information about the target and can be as simple as viewing a target's publicly available social media profile. Example information that we might collect includes domain names, IP address blocks, email addresses, employee names, and job posts. In the upcoming task, we'll see how to query DNS records and expand on the topics from the Passive Reconnaissance room and introduce advanced tooling to aid in your recon.

Active recon requires interacting with the target by sending requests and packets and observing if and how it responds. The responses collected - or lack of responses - would enable us to expand on the picture we started developing using passive recon. An example of active reconnaissance is using Nmap to scan target subnets and live hosts. Other examples can be found in the Active Reconnaissance room. Some information that we would want to discover include live hosts, running servers, listening services, and version numbers.

Active recon can be classified as:

1. **External Recon:** Conducted outside the target's network and focuses on the externally facing assets assessable from the Internet. One example is running Nikto from outside the company network.
2. **Internal Recon:** Conducted from within the target company's network. In other words, the pentester or red teamer might be physically located inside the company building. In this scenario, they might be using an exploited host on the target's network. An example would be using Nessus to scan the internal network using one of the target’s computers.

**_Answer the questions below_**

1. **Ensure you have a clear understanding of the different types of recon activities before proceeding.**

- **_Ans: No Answer Needed_**

---

### Task 3: Built-in Tools

This task focuses on:

- `whois`
- `dig, nslookup, host`
- `traceroute/tracert`

Before we start using the whois tool, let's look at WHOIS. WHOIS is a request and response protocol that follows the RFC 3912 specification. A WHOIS server listens on TCP port 43 for incoming requests. The domain registrar is responsible for maintaining the WHOIS records for the domain names it is leasing. whois will query the WHOIS server to provide all saved records. In the following example, we can see whois provides us with:

- Registrar WHOIS server
- Registrar URL
- Record creation date
- Record update date
- Registrant contact info and address (unless withheld for privacy)
- Admin contact info and address (unless withheld for privacy)
- Tech contact info and address (unless withheld for privacy)

```

pentester@TryHackMe$ whois thmredteam.com
[Querying whois.verisign-grs.com]
[Redirected to whois.namecheap.com]
[Querying whois.namecheap.com]
[whois.namecheap.com]
Domain name: thmredteam.com
Registry Domain ID: 2643258257_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.namecheap.com
Registrar URL: http://www.namecheap.com
Updated Date: 0001-01-01T00:00:00.00Z
Creation Date: 2021-09-24T14:04:16.00Z
Registrar Registration Expiration Date: 2022-09-24T14:04:16.00Z
Registrar: NAMECHEAP INC
Registrar IANA ID: 1068
Registrar Abuse Contact Email: abuse@namecheap.com
Registrar Abuse Contact Phone: +1.6613102107
Reseller: NAMECHEAP INC
Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
Registry Registrant ID:
Registrant Name: Withheld for Privacy Purposes
Registrant Organisation: Privacy service provided by Withheld for Privacy ehf
Registrant Street: Kalkofnsvegur 2
Registrant City: Reykjavik
Registrant State/Province: Capital Region
Registrant Postal Code: 101
Registrant Country: IS
Registrant Phone: +354.4212434
Registrant Phone Ext:
Registrant Fax:
Registrant Fax Ext:
Registrant Email: 4c9d5617f14e4088a4396b2f25430925.protect@withheldforprivacy.com
Registry Admin ID:
Admin Name: Withheld for Privacy Purposes
[...]
Tech Name: Withheld for Privacy Purposes
[...]
Name Server: kip.ns.cloudflare.comName Server: uma.ns.cloudflare.com
DNSSEC: unsigned
URL of the ICANN WHOIS Data Problem Reporting System: http://wdprs.internic.net/
>>> Last update of WHOIS database: 2021-10-13T10:42:40.11Z <<<
For more information on Whois status codes, please visit https://icann.org/epp

```

As we can see above, it is possible to gain a lot of valuable information with only a domain name. After a whois lookup, we might get lucky and find names, email addresses, postal addresses, and phone numbers, in addition to other technical information. At the end of the whois query, we find the authoritative name servers for the domain in question.

DNS queries can be executed with many different tools found on our systems, especially Unix-like systems. One common tool found on Unix-like systems, Windows, and macOS is nslookup. In the following query, we can see how nslookup uses the default DNS server to get the A and AAAA records related to our domain.

```
pentester@TryHackMe$ nslookup cafe.thmredteam.com
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
Name:	cafe.thmredteam.com
Address: 104.21.93.169
Name:	cafe.thmredteam.com
Address: 172.67.212.249
Name:	cafe.thmredteam.com
Address: 2606:4700:3034::ac43:d4f9
Name:	cafe.thmredteam.com
Address: 2606:4700:3034::6815:5da9

```

Another tool commonly found on Unix-like systems is `dig`, short for Domain Information Groper (dig). dig provides a lot of query options and even allows you to specify a different DNS server to use. For example, we can use Cloudflare's DNS server: `dig @1.1.1.1 tryhackme.com.`

```

pentester@TryHackMe$ dig cafe.thmredteam.com @1.1.1.1

; <<>> DiG 9.16.21-RH <<>> cafe.thmredteam.com @1.1.1.1
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16698
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;cafe.thmredteam.com.		IN	A

;; ANSWER SECTION:
cafe.thmredteam.com.	3114	IN	A	104.21.93.169
cafe.thmredteam.com.	3114	IN	A	172.67.212.249

;; Query time: 4 msec
;; SERVER: 1.1.1.1#53(1.1.1.1)
;; WHEN: Thu Oct 14 10:44:11 EEST 2021
;; MSG SIZE  rcvd: 80

```

`host` is another useful alternative for querying DNS servers for DNS records. Consider the following example.

```
pentester@TryHackMe$ host cafe.thmredteam.com
cafe.thmredteam.com has address 172.67.212.249
cafe.thmredteam.com has address 104.21.93.169
cafe.thmredteam.com has IPv6 address 2606:4700:3034::ac43:d4f9
cafe.thmredteam.com has IPv6 address 2606:4700:3034::6815:5da9

```

The final tool that ships with Unix-like systems is `traceroute`, or on MS Windows systems, tracert. As the name indicates, it traces the route taken by the packets from our system to the target host. The console output below shows that `traceroute` provided us with the routers (hops) connecting us to the target system. It's worth stressing that some routers don’t respond to the packets sent by `traceroute`, and as a result, we don’t see their IP addresses; a is used to indicate such a case.

```

pentester@TryHackMe$ traceroute cafe.thmredteam.com
traceroute to cafe.thmredteam.com (172.67.212.249), 30 hops max, 60 byte packets
 1  _gateway (192.168.0.1)  3.535 ms  3.450 ms  3.398 ms
 2  * * *
 3  * * *
 4  * * *
 5  * * *
 6  * * *
 7  172.16.79.229 (172.16.79.229)  4.663 ms  6.417 ms  6.347 ms
 8  * * *
 9  172.16.49.1 (172.16.49.1)  6.688 ms 172.16.48.1 (172.16.48.1)  6.671 ms 172.16.49.1 (172.16.49.1)  6.651 ms
10  213.242.116.233 (213.242.116.233)  96.769 ms 81.52.187.243 (81.52.187.243)  96.634 ms  96.614 ms
11  bundle-ether302.pastr4.paris.opentransit.net (193.251.131.116)  96.592 ms  96.689 ms  96.671 ms
12  193.251.133.251 (193.251.133.251)  96.679 ms  96.660 ms  72.465 ms
13  193.251.150.10 (193.251.150.10)  72.392 ms 172.67.212.249 (172.67.212.249)  91.378 ms  91.306 ms

```

In summary, we can always rely on:

- whois to query the WHOIS database
- nslookup, dig, or host to query DNS servers

WHOIS databases and DNS servers hold publicly available information, and querying either does not generate any suspicious traffic.

Moreover, we can rely on Traceroute (traceroute on Linux and macOS systems and tracert on MS Windows systems) to discover the hops between our system and the target host.

**_Answer the questions below_**

1. **When was thmredteam.com created (registered)? (YYYY-MM-DD)**

- **_2021-09-24_**

2. **To how many IPv4 addresses does clinic.thmredteam.com resolve?**

- **_2_**

3. **To how many IPv6 addresses does clinic.thmredteam.com resolve?**

- **_2_**

![Tools](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Red-Team-Recon/Picture-2.png)

---

### Task 4 Advanced Searching

Being able to use a search engine efficiently is a crucial skill. The following table shows some popular search modifiers that work with many popular search engines.

| Symbol / Syntax                  | Function                                            |
| -------------------------------- | --------------------------------------------------- |
| `"search phrase"`                | Find results with exact search phrase               |
| `OSINT filetype:pdf`             | Find files of type `PDF` related to a certain term. |
| `salary site:blog.tryhackme.com` | Limit search results to a specific site.            |
| `pentest -site:example.com`      | Exclude a specific site from results                |
| `walkthrough intitle:TryHackMe`  | Find pages with a specific term in the page title.  |
| `challenge inurl:tryhackme`      | Find pages with a specific term in the page URL.    |

Note: In addition to pdf, other filetypes to consider are: doc, docx, ppt, pptx, xls and xlsx.

Each search engine might have a slightly varied set of rules and syntax. To learn about the specific syntax for the different search engines, you will need to visit their respective help pages. Some search engines, such as Google, provide a web interface for advanced searches: Google Advanced Search. Other times, it is best to learn the syntax by heart, such as Google Refine Web Searches, DuckDuckGo Search Syntax, and Bing Advanced Search Options.

Search engines crawl the world wide web day and night to index new web pages and files. Sometimes this can lead to indexing confidential information. Examples of confidential information include:

- Documents for internal company use
- Confidential spreadsheets with usernames, email addresses, and even passwords
- Files containing usernames
- Sensitive directories
- Service version number (some of which might be vulnerable and unpatched)
- Error messages

Combining advanced Google searches with specific terms, documents containing sensitive information or vulnerable web servers can be found. Websites such as Google Hacking Database (GHDB) collect such search terms and are publicly available. Let's take a look at some of the GHDB queries to see if our client has any confidential information exposed via search engines. GHDB contains queries under the following categories:

- **Footholds**
  Consider GHDB-ID: 6364 as it uses the query `intitle:"index of" "nginx.log"` to discover Nginx logs and might reveal server misconfigurations that can be exploited.
- **Files Containing Usernames**
  For example, GHDB-ID: 7047 uses the search term `intitle:"index of" "contacts.txt"` to discover files that leak juicy information.
- **Sensitive Directories**
  For example, consider GHDB-ID: 6768, which uses the search term `inurl:/certs/server.key` to find out if a private RSA key is exposed.
- **Web Server Detection**
  Consider GHDB-ID: 6876, which detects GlassFish Server information using the query `intitle:"GlassFish Server - Server Running".`
- **Vulnerable Files**
  For example, we can try to locate PHP files using the query `intitle:"index of" "\*.php"`, as provided by GHDB-ID: 7786.
- **Vulnerable Servers**
  For instance, to discover SolarWinds Orion web consoles, GHDB-ID: 6728 uses the query `intext:"user name" intext:"orion core" -solarwinds.com.`
- **Error Messages**
  Plenty of useful information can be extracted from error messages. One example is GHDB-ID: 5963, which uses the query `intitle:"index of" errors.log` to find log files related to errors.

You might need to adapt these Google queries to fit your needs as the queries will return results from all web servers that fit the criteria and were indexed. To avoid legal issues, it is best to refrain from accessing any files outside the scope of your legal agreement.

We recommend you join the Google Dorking room for more in-depth information.

Now we'll explore two additional sources that can provide valuable information without interacting with our target:

- Social Media
- Job ads

![Social Media](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Red-Team-Recon/Picture-3.jpg)

**Social Media**

Social media websites have become very popular for not only personal use but also for corporate use. Some social media platforms can reveal tons of information about the target. This is especially true as many users tend to overshare details about themselves and their work. To name a few, it's worthwhile checking the following:

- LinkedIn
- Twitter
- Facebook
- Instagram

Social media websites make it easy to collect the names of a given company's employees; moreover, in certain instances, you might learn specific pieces of information that can reveal answers to password recovery questions or gain ideas to include in a targeted wordlist. Posts from technical staff might reveal details about a company’s systems and vendors. For example, a network engineer who was recently issued Juniper certifications may allude to Juniper networking infrastructure being used in their employer’s environment.

![Social Media](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Red-Team-Recon/Picture-4.jpg)


**Job Ads**

Job advertisements can also tell you a lot about a company. In addition to revealing names and email addresses, job posts for technical positions could give insight into the target company’s systems and infrastructure. The popular job posts might vary from one country to another. Make sure to check job listing sites in the countries where your client would post their ads. Moreover, it is always worth checking their website for any job opening and seeing if this can leak any interesting information.

Note that the Wayback Machine can be helpful to retrieve previous versions of a job opening page on your client’s site.

***Answer the questions below***

1. **How would you search using Google for xls indexed for http://clinic.thmredteam.com?**
- **filetype:xls site:clinic.thmredteam.com**

2. **How would you search using Google for files with the word passwords for http://clinic.thmredteam.com?**
- **passwords site:clinic.thmredteam.com**

---

### Task 5 Specialized Search Engines

**WHOIS and DNS Related**

Beyond the standard WHOIS and DNS query tools that we covered in Task 3, there are third parties that offer paid services for historical WHOIS data. One example is WHOIS history, which provides a history of WHOIS data and can come in handy if the domain registrant didn’t use WHOIS privacy when they registered the domain.

There are a handful of websites that offer advanced DNS services that are free to use. Some of these websites offer rich functionality and could have a complete room dedicated to exploring one domain. For now, we'll focus on key DNS related aspects. We will consider the following:

- VidewDNS.info
- Threat Intelligence Platform

**ViewDNS.info**

VidewDNS.info offers Reverse IP Lookup. Initially, each web server would use one or more IP addresses; however, today, it is common to come across shared hosting servers. With shared hosting, one IP address is shared among many different web servers with different domain names. With reverse IP lookup, starting from a domain name or an IP address, you can find the other domain names using a specific IP address(es).

In the figure below, we used reverse IP lookup to find other servers sharing the same IP addresses used by cafe.thmredteam.com. Therefore, it is important to note that knowing the IP address does not necessarily lead to a single website.

![View DNS](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Red-Team-Recon/Picture-5.png)


**Threat Intelligence Platform**

Threat Intelligence Platform requires you to provide a domain name or an IP address, and it will launch a series of tests from malware checks to WHOIS and DNS queries. The WHOIS and DNS results are similar to the results we would get using whois and dig, but Threat Intelligence Platform presents them in a more readable and visually appealing way. There is extra information that we get with our report. For instance, after we look up thmredteam.com, we see that Name Server (NS) records were resolved to their respective IPv4 and IPv6 addresses, as shown in the figure below.

![Threat](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Red-Team-Recon/Picture-6.png)

On the other hand, when we searched for cafe.thmredteam.com, we could also get a list of other domains on the same IP address. The result we see in the figure below is similar to the results we obtained using VidewDNS.info.

![Threat](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Red-Team-Recon/Picture-7.png)


**Specialized Search Engines**
**Censys**

Censys Search can provide a lot of information about IP addresses and domains. In this example, we look up one of the IP addresses that cafe.thmredteam.com resolves to. We can easily infer that the IP address we looked up belongs to Cloudflare. We can see information related to ports 80 and 443, among others; however, it's clear that this IP address is used to server websites other than cafe.thmredteam.com. In other words, this IP address belongs to a company other than our client, Organic Cafe. It's critical to make this distinction so that we don’t probe systems outside the scope of our contract.

![Censys](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Red-Team-Recon/Picture-8.png)



***Answer the questions below***

1. **What is the shodan command to get your Internet-facing IP address?**
- **shodan myip**

![Shodan](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Red-Team-Recon/Picture-9.png)

### Task 6 Recon-ng 

Recon-ng is a framework that helps automate the OSINT work. It uses modules from various authors and provides a multitude of functionality. Some modules require keys to work; the key allows the module to query the related online API. In this task, we will demonstrate using Recon-ng in the terminal.

From a penetration testing and red team point of view, Recon-ng can be used to find various bits and pieces of information that can aid in an operation or OSINT task. All the data collected is automatically saved in the database related to your workspace. For instance, you might discover host addresses to later port-scan or collect contact email addresses for phishing attacks.

You can start Recon-ng by running the command recon-ng. Starting Recon-ng will give you a prompt like [recon-ng][default] >. At this stage, you need to select the installed module you want to use. However, if this is the first time you're running recon-ng, you will need to install the module(s) you need.

In this task, we will follow the following workflow:

- Create a workspace for your project
- Insert the starting information into the database
- Search the marketplace for a module and learn about it before installing
- List the installed modules and load one
- Run the loaded module

Creating a Workspace

Run workspaces create WORKSPACE_NAME to create a new workspace for your investigation. For example, workspaces create thmredteam will create a workspace named thmredteam.

recon-ng -w WORKSPACE_NAME starts recon-ng with the specific workspace.
Seeding the Database

In reconnaissance, you are starting with one piece of information and transforming it into new pieces of information. For instance, you might start your research with a company name and use that to discover the domain name(s), contacts and profiles. Then you would use the new information you obtained to transform it further and learn more about your target.

Let’s consider the case where we know the target's domain name, thmredteam.com, and we would like to feed it into the Recon-ng database related to the active workspace. If we want to check the names of the tables in our database, we can run db schema.

We want to insert the domain name thmredteam.com into the domains table. We can do this using the command db insert domains.
Pentester Terminal

```         
pentester@TryHackMe$ recon-ng -w thmredteam
[...]
[recon-ng][thmredteam] > db insert domains
domain (TEXT): thmredteam.com
notes (TEXT): 
[*] 1 rows affected.
[recon-ng][thmredteam] > marketplace search
```

        

Recon-ng Marketplace

We have a domain name, so a logical next step would be to search for a module that transforms domains into other types of information. Assuming we are starting from a fresh installation of Recon-ng, we will search for suitable modules from the marketplace.

Before you install modules using the marketplace, these are some useful commands related to marketplace usage:

- marketplace search KEYWORD to search for available modules with keyword.
- marketplace info MODULE to provide information about the module in question.
- marketplace install MODULE to install the specified module into Recon-ng.
- marketplace remove MODULE to uninstall the specified module.

The modules are grouped under multiple categories, such as discovery, import, recon and reporting. Moreover, recon is also divided into many subcategories depending on the transform type. Run marketplace search to get a list of all available modules.

In the terminal below, we search for modules containing domains-.
Pentester Terminal

```         
pentester@TryHackMe$ recon-ng -w thmredteam
[...]
[recon-ng][thmredteam] > marketplace search domains-
[*] Searching module index for 'domains-'...

  +---------------------------------------------------------------------------------------------------+
  |                        Path                        | Version |     Status    |  Updated   | D | K |
  +---------------------------------------------------------------------------------------------------+
  | recon/domains-companies/censys_companies           | 2.0     | not installed | 2021-05-10 | * | * |
  | recon/domains-companies/pen                        | 1.1     | not installed | 2019-10-15 |   |   |
  | recon/domains-companies/whoxy_whois                | 1.1     | not installed | 2020-06-24 |   | * |
  | recon/domains-contacts/hunter_io                   | 1.3     | not installed | 2020-04-14 |   | * |
  | recon/domains-contacts/metacrawler                 | 1.1     | not installed | 2019-06-24 | * |   |
  | recon/domains-contacts/pen                         | 1.1     | not installed | 2019-10-15 |   |   |
  | recon/domains-contacts/pgp_search                  | 1.4     | not installed | 2019-10-16 |   |   |
  | recon/domains-contacts/whois_pocs                  | 1.0     | not installed | 2019-06-24 |   |   |
  | recon/domains-contacts/wikileaker                  | 1.0     | not installed | 2020-04-08 |   |   |
  | recon/domains-credentials/pwnedlist/account_creds  | 1.0     | not installed | 2019-06-24 | * | * |
  | recon/domains-credentials/pwnedlist/api_usage      | 1.0     | not installed | 2019-06-24 |   | * |
  | recon/domains-credentials/pwnedlist/domain_creds   | 1.0     | not installed | 2019-06-24 | * | * |
  | recon/domains-credentials/pwnedlist/domain_ispwned | 1.0     | not installed | 2019-06-24 |   | * |
  | recon/domains-credentials/pwnedlist/leak_lookup    | 1.0     | not installed | 2019-06-24 |   |   |
  | recon/domains-credentials/pwnedlist/leaks_dump     | 1.0     | not installed | 2019-06-24 |   | * |
  | recon/domains-domains/brute_suffix                 | 1.1     | not installed | 2020-05-17 |   |   |
  | recon/domains-hosts/binaryedge                     | 1.2     | not installed | 2020-06-18 |   | * |
  | recon/domains-hosts/bing_domain_api                | 1.0     | not installed | 2019-06-24 |   | * |
  | recon/domains-hosts/bing_domain_web                | 1.1     | not installed | 2019-07-04 |   |   |
  | recon/domains-hosts/brute_hosts                    | 1.0     | not installed | 2019-06-24 |   |   |
  | recon/domains-hosts/builtwith                      | 1.1     | not installed | 2021-08-24 |   | * |
  | recon/domains-hosts/censys_domain                  | 2.0     | not installed | 2021-05-10 | * | * |
  | recon/domains-hosts/certificate_transparency       | 1.2     | not installed | 2019-09-16 |   |   |
  | recon/domains-hosts/google_site_web                | 1.0     | not installed | 2019-06-24 |   |   |
  | recon/domains-hosts/hackertarget                   | 1.1     | not installed | 2020-05-17 |   |   |
  | recon/domains-hosts/mx_spf_ip                      | 1.0     | not installed | 2019-06-24 |   |   |
  | recon/domains-hosts/netcraft                       | 1.1     | not installed | 2020-02-05 |   |   |
  | recon/domains-hosts/shodan_hostname                | 1.1     | not installed | 2020-07-01 | * | * |
  | recon/domains-hosts/spyse_subdomains               | 1.1     | not installed | 2021-08-24 |   | * |
  | recon/domains-hosts/ssl_san                        | 1.0     | not installed | 2019-06-24 |   |   |
  | recon/domains-hosts/threatcrowd                    | 1.0     | not installed | 2019-06-24 |   |   |
  | recon/domains-hosts/threatminer                    | 1.0     | not installed | 2019-06-24 |   |   |
  | recon/domains-vulnerabilities/ghdb                 | 1.1     | not installed | 2019-06-26 |   |   |
  | recon/domains-vulnerabilities/xssed                | 1.1     | not installed | 2020-10-18 |   |   |
  +---------------------------------------------------------------------------------------------------+

  D = Has dependencies. See info for details.
  K = Requires keys. See info for details.

[recon-ng][thmredteam] >
```

We notice many subcategories under recon, such as domains-companies, domains-contacts, and domains-hosts. This naming tells us what kind of new information we will get from that transformation. For instance, domains-hosts means that the module will find hosts related to the provided domain.

Some modules, like whoxy_whois, require a key, as we can tell from the * under the K column. This requirement indicates that this module is not usable unless we have a key to use the related service.

Other modules have dependencies, indicated by a * under the D column. Dependencies show that third-party Python libraries might be necessary to use the related module.

Let’s say that you are interested in recon/domains-hosts/google_site_web. To learn more about any particular module, you can use the command marketplace info MODULE; this is an essential command that explains what the module does. For example, marketplace info google_site_web provides the following description: “Harvests hosts from Google.com by using the ‘site’ search operator. Updates the ‘hosts’ table with the results.” In other words, this module will use the Google search engine and the “site” operator.

We can install the module we want with the command marketplace install MODULE, for example, marketplace install google_site_web.
Working with Installed Modules

We can work with modules using:

- modules search to get a list of all the installed modules
- modules load MODULE to load a specific module to memory

Let’s load the module that we installed earlier from the marketplace, modules load viewdns_reverse_whois. To run it, we need to set the required options.

- options list to list the options that we can set for the loaded module.
- options set <option> <value> to set the value of the option.

In a previous step, we have installed the module google_site_web, so let’s load it using load google_site_web and run it with run. We have already added the domain thmredteam.com to the database, so when the module is run, it will read that value from the database, get new kinds of information, and add them to the database in turn. The commands and the results are shown in the terminal output below.
Pentester Terminal

```        
pentester@TryHackMe$ recon-ng -w thmredteam
[...]
[recon-ng][thmredteam] > load google_site_web
[recon-ng][thmredteam][google_site_web] > run

--------------
THMREDTEAM.COM
--------------
[*] Searching Google for: site:thmredteam.com
[*] Country: None
[*] Host: cafe.thmredteam.com
[*] Ip_Address: None
[*] Latitude: None
[*] Longitude: None
[*] Notes: None
[*] Region: None
[*] --------------------------------------------------
[*] Country: None
[*] Host: clinic.thmredteam.com
[*] Ip_Address: None
[*] Latitude: None
[*] Longitude: None
[*] Notes: None
[*] Region: None
[*] --------------------------------------------------
[...]
[*] 2 total (2 new) hosts found.
[recon-ng][thmredteam][google_site_web] >
```
        

This module has queried Google and discovered two hosts, cafe.thmredteam.com and clinic.thmredteam.com. It is possible that by the time you run these steps, new hosts will also appear.
Keys

Some modules cannot be used without a key for the respective service API. K indicates that you need to provide the relevant service key to use the module in question.

    keys list lists the keys
    keys add KEY_NAME KEY_VALUE adds a key
    keys remove KEY_NAME removes a key

Once you have the set of modules installed, you can proceed to load and run them.

    modules load MODULE loads an installed module
    CTRL + C unloads the module.
    info to review the loaded module’s info.
    options list lists available options for the chosen module.
    options set NAME VALUE
    run to execute the loaded module.

Demo

To wrap up, use the following demonstration provided below containing all the steps we have explained earlier.
Use recon-ng to repeat the steps we carried out against thmredteam.com, then answer the following questions.

***Answer the questions below***

1. **How do you start recon-ng with the workspace clinicredteam?**
- **recon-ng -w clinicredteam**

2. **How many modules with the name virustotal exist?**
- **2**

3. **There is a single module under hosts-domains. What is its name?**
- **migrate_hosts**

4. **censys_email_address is a module that “retrieves email addresses from the TLS certificates for a company.” Who is the author?**
- **Censys Team**

![Recon-Ng](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Red-Team-Recon/Picture-10.png)

![Recon-Ng](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Red-Team-Recon/Picture-10.png)

![Recon-Ng](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Red-Team-Recon/Picture-11.png)

---

### Task 8 Summary 


Sun Tzu once said, “If you know the enemy and know yourself, you need not fear the result of a hundred battles. If you know yourself but not the enemy, for every victory gained you will also suffer a defeat. If you know neither the enemy nor yourself, you will succumb in every battle.” Fast forward to the cyber warfare era; in addition to knowing our red team skillset and capabilities, we need to gain as much information about the target as possible. The terrain is constantly evolving, and new ways to collect data are becoming possible.

We have reviewed essential built-in tools such as whois, dig, and tracert. Moreover, we explored the power of search engines to aid in our passive reconnaissance activities. Finally, we demonstrated two tools, Recon-ng and Maltego, that allow us to collect information from various sources and present them in one place.

The purpose is to expand our knowledge about the target and collect various information that can be leveraged in the subsequent attack phases. For instance, hosts that are discovered can be scanned and probed for vulnerabilities, while contact information and email addresses can be used to launch phishing campaigns efficiently. In brief, the more information we gather about the target, the more we can refine our attacks and increase our chances of success.

***Answer the questions***

1. **The different tools and websites presented in this room provide the basics necessary to tackle further reconnaissance work.**

- ***No Answer Needed***