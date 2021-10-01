# Burp Suite: The Basics

#### An introduction to using Burp Suite for Web Application pentesting.

### Task 1: Introduction Outline

Welcome to Burp Suite Basics!
This room will cover the foundations of using the Burp Suite web application framework.

Specifically, we will be looking at:

- What Burp Suite is
- An overview of the available tools in the framework
- Installing Burp Suite for yourself
- Navigating and configuring Burp Suite.

We will also be introducing the core of the Burp Suite framework: the Burp Proxy. This room is primarily designed to provide a foundational knowledge of Burp Suite which can then be built upon further in the other rooms of the Burp module; as such, it will be a lot heavier in theory than subsequent rooms, which take more of a practical approach. You are advised to read the information here and follow along yourself with a copy of the tool if you haven't used Burp Suite before. Experimentation is key: use this information in tandem with playing around with the app for yourself to build a foundation for using the framework, which can then be built upon in later rooms.

Let's begin!

**_Answer the questions below_**

1. **Deploy the machine (and the AttackBox if you are not using your own attack VM), and let's get started!**

**Note: If you are not using the AttackBox and want to connect to this machine without the VPN, you can do so using this link once the machine has fully loaded and an IP address is displayed: https://10-10-94-216.p.thmlabs.com.**

- **_No Answer Needed._**

---

### Task 2: Task 2 Getting Started What is Burp Suite?

Put simply: Burp Suite is a framework written in Java that aims to provide a one-stop-shop for web application penetration testing. In many ways, this goal is achieved as Burp is very much the industry standard tool for hands-on web app security assessments. Burp Suite is also very commonly used when assessing mobile applications, as the same features which make it so attractive for web app testing translate almost perfectly into testing the APIs (Application Programming Interfaces) powering most mobile apps.

At the simplest level, Burp can capture and manipulate all of the traffic between an attacker and a webserver: this is the core of the framework. After capturing requests, we can choose to send them to various other parts of the Burp Suite framework -- we will be covering some of these tools in upcoming rooms. This ability to intercept, view, and modify web requests prior to them being sent to the target server (or, in some cases, the responses before they are received by our browser), makes Burp Suite perfect for any kind of manual web app testing.

There are various different editions of Burp Suite available. We will be working with the Burp Suite Community edition, as this is free to use for any (legal) non-commercial use. The Burp Suite Professional and Enterprise editions both require expensive licenses but come with powerful extra features:

- **Burp Suite Professional** is an unrestricted version of Burp Suite Community. It comes with features such as:

* An automated vulnerability scanner
* A fuzzer/bruteforcer that isn't rate limited
* Saving projects for future use; report generation
* A built-in API to allow integration with other tools
* Unrestricted access to add new extensions for greater functionality
* Access to the Burp Suite Collaborator (effectively providing a unique request catcher self-hosted or running on a Portswigger owned server)

In short, Burp Pro is an extremely powerful tool -- which is why it comes with a £319/$399 price tag per user for a one-year subscription. For this reason, Burp Pro is usually only used by professionals (with licenses often being provided by employers).

- **Burp Suite Enterprise** is slightly different. Unlike the community and professional editions, Burp Enterprise is used for continuous scanning. It provides an automated scanner that can periodically scan webapps for vulnerabilities in much the same way as software like Nessus performs automated infrastructure scanning. Unlike the other editions of Burp Suite which allow you to perform manual attacks from your own computer, Enterprise sits on a server and constantly scans target web apps for vulnerabilities.

Due to the prohibitive costs involved with either of these editions of Burp Suite, we will stick to the core feature-set provided by Burp Suite Community.

Note: Burp Suite for Windows is featured in the screenshots for many demonstrations; however, there are no differences between this and the copy of Burp Suite installed on the AttackBox.

**_Answer the questions below_**

1. **Which edition of Burp Suite will we be using in this module?.**

- **_Ans: Burp Suite Community._**

2. **Which edition of Burp Suite runs on a server and provides constant scanning for target web apps?.**

- **_Ans: Burp Suite Enterprise._**

3. **Burp Suite is frequently used when attacking web applications and **\_\_** applications.**

- **_Ans: Mobile._**

---

### Task 3: Getting Started Features of Burp Community

Whilst Burp Community has a relatively limited feature-set compared to the Professional edition, it still has many superb tools available. These include:

**Proxy**: The most well-known aspect of Burp Suite, the Burp Proxy allows us to intercept and modify requests/responses when interacting with web applications.

**Repeater**: The second most well-known Burp feature -- Repeater -- allows us to capture, modify, then resend the same request numerous times. This feature can be absolutely invaluable, especially when we need to craft a payload through trial and error (e.g. in an SQLi -- Structured Query Language Injection) or when testing the functionality of an endpoint for flaws.

**Intruder**: Although harshly rate-limited in Burp Community, Intruder allows us to spray an endpoint with requests. This is often used for bruteforce attacks or to fuzz endpoints.

**Decoder**: Though less-used than the previously mentioned features, Decoder still provides a valuable service when transforming data -- either in terms of decoding captured information, or encoding a payload prior to sending it to the target. Whilst there are other services available to do the same job, doing this directly within Burp Suite can be very efficient.

**Comparer**: As the name suggests, Comparer allows us to compare two pieces of data at either word or byte level. Again, this is not something that is unique to Burp Suite, but being able to send (potentially very large) pieces of data directly into a comparison tool with a single keyboard shortcut can speed things up considerably.

**Sequencer**: We usually use Sequencer when assessing the randomness of tokens such as session cookie values or other supposedly random generated data. If the algorithm is not generating secure random values, then this could open up some devastating avenues for attack.

In addition to the myriad of in-built features, the Java codebase also makes it very easy to write extensions to add to the functionality of the Burp framework. These can be written in Java, Python (using the Java Jython interpreter), or Ruby (using the Java JRuby interpreter). The Burp Suite Extender module can quickly and easily load extensions into the framework, as well as providing a marketplace to download third-party modules (referred to as the "BApp Store"). Whilst many of these extensions require a professional license to download and add in, there are still a fair number that can be integrated with Burp Community. For example, we may wish to extend the inbuilt logging functionality of Burp Suite with the Logger++ module.

**_Answer the questions below_**

1. **Which Burp Suite feature allows us to intercept requests between ourselves and the target?.**

- **_Ans: Proxy._**

2. **Which Burp tool would we use if we wanted to bruteforce a login form?.**

- **_Ans: Intruder._**

---

### Task 4: Getting Started Installation

Burp Suite is one of those tools that is very useful to have around, whether you're explicitly assessing a web or mobile application for a pentest/bug bounty, or are simply wanting to debug a new feature in a web app you are developing. For this reason, it is important to know how to install Burp Suite on a variety of platforms, rather than just using it inside a pentesting OS such as Kali or Parrot. You never know when you might need it!

Fortunately, [PortSwigger](https://portswigger.net/) have made installing Burp Suite extremely easy on Linux, macOS, and Windows, providing dedicated installers for all three. As a Java application, Burp can also be downloaded as a JAR archive and run on effectively anything that will support a Java runtime environment.

Burp Suite comes pre-packaged with Kali Linux, so you should not need to install it there. If, for some reason, Burp is missing from your Kali installation, you can easily install it from the Kali `apt` repositories.

For other systems, we can download installers from the [Burp Suite Downloads page](https://portswigger.net/burp/releases/community/latest).

From the dropdown menus, we can select our operating system, as well as whether we want Burp Suite Community or Burp Suite Professional:

![Burp Suite Download](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-1.png)

We can then click the "Download" button to start downloading the Burp Suite installer. No matter which operating system you are using, make sure to use Burp Suite Community Edition.
Once we have verified the integrity of our download, we can install it in the normal way for our operating system (e.g. Running the executable in Windows or executing the script from the terminal with `sudo` in Linux).

Note: If installing in Linux, you can choose to install either with or without super-user permissions. If you decide not to use `sudo` when executing the script, Burp Suite will be installed in your home directory at `~/BurpSuiteCommunity/BurpSuiteCommunity` and will not be added to your `PATH.`

The installation wizard is very intuitive. It is generally safe to accept the suggested defaults, regardless of your operating system; however, it is still sensible to read through the installer carefully.

With Burp Suite installed, we can now start up the application. The first time we use it, Burp Suite will ask us to read and accept its terms and conditions; make sure you do so before accepting or declining them!

With the terms and conditions accepted, we are presented with another menu. We will go through this in the next task.

**_Answer the questions below_**

1. **If you have chosen not to use the AttackBox, make sure that you have a copy of Burp Suite installed before proceeding..**

- **_Ans: No Answer Needed._**

---

### Task 5: Getting Started The Dashboard

When we open Burp Suite and have accepted the terms and conditions, we are met with a window asking us to select the project type.

This window doesn't give us many options in Burp Community. Burp Pro would allow us to save our work to the disk or load a previously saved project at this point. All we can do here is click "Next", however.

The next window allows us to choose a configuration for Burp Suite. Leaving this at the default is perfect for most situations:

Click "Start Burp", and the main Burp Suite interface will open!

The first time you open Burp Suite, you may be presented with a screen of training options. These are well worth reading through if you get the time.

If not (and in any subsequent sessions regardless), you will be presented with the slightly daunting Burp Dashboard:

![Burp Suite Dashboard](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-2.png)

![Burp Suite Dashboard](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-3.png)

Don't be alarmed if this doesn't make too much sense just yet -- it soon will!

In short, the Dashboard interface is split into four quadrants:

![Burp Suite Dashboard](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-4.png)

1. The Tasks menu allows us to define background tasks that Burp Suite will run whilst we use the application. The Pro version would also allow us to create on-demand scans. The default "Live Passive Crawl" (which automatically logs the pages we visit) will be more than suitable for our uses in this module.
2. The Event log tells us what Burp Suite is doing (e.g. starting the Proxy), as well as information about any connections that we are making through Burp.
3. The Issue Activity section is exclusive to Burp Pro. It won't give us anything using Burp Community, but in Burp Professional it would list all of the vulnerabilities found by the automated scanner. These would be ranked by severity and filterable by how sure Burp is that the component is vulnerable.
4. The Advisory section gives more information about the vulnerabilities found, as well as references and suggested remediations. These could then be exported into a report.
   Clicking on one of the example vulnerabilities in the Issue Activity section gives us an idea of what this looks like:

![Burp Suite Dashboard](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-5.png)

Throughout the various tabs and windows of Burp Suite, you will find little help icons: a question mark within a circle.

Clicking on these will open a new window containing help for the section, for example:

![Burp Suite Dashboard](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-6.png)

These are extremely useful if you're ever stuck and don't know what a feature does, so make good use of them!

**_Answer the questions below_**

1. **Open Burp Suite and have a look around the dashboard. Make sure that you are comfortable with it before moving on..**

- **_Ans: No Answer Needed._**

---

### Task 6: Getting Started Navigation

Navigating around the Burp Suite GUI by default is done entirely using the top menu bars:

![Burp Suite Proxy](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-7.png)

These allow you to switch between modules (along the top row of the attached image). If the selected module has more than one sub-tab, then these can be selected using a second menu bar which appears directly below the original bar (the bottom row of the image above). It is common for module-specific settings to be provided in these sub-tabs (as is the case with the Proxy Options above).

Tabs can also be popped out into separate windows should you prefer to view multiple tabs separately. This can be done by clicking "Window" in the application menu at the top of the screen, then choosing to "Detach" tabs:

![Burp Suite Window](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-8.png)

These can be reattached in the same way.

In addition to the menu bar, Burp Suite also has keyboard shortcuts that allow quick navigation to key tabs. By default, these are:

| **Shortcut**<br>        | **Does**<br>                   |
| ----------------------- | ------------------------------ |
| `Ctrl + Shift + D`<br>  | Switch to the Dashboard<br>    |
| `Ctrl + Shift + T`<br>  | Switch to the Target tab<br>   |
| `Ctrl + Shift + P`<br>  | Switch to the Proxy tab<br>    |
| `Ctrl + Shift + I` <br> | Switch to the Intruder tab<br> |
| `Ctrl + Shift + R` <br> | Switch to the Repeater tab<br> |

We will look at how we can view and change these in the next task.

**_Answer the questions below_**

1. **Get comfortable navigating around the top menu bars**

- **_Ans: No Answer Needed._**

---

### Task 7: Getting Started Options

Before we start learning about the Burp Proxy, let's take a look at the options available for configuring Burp Suite.

- Global settings can be found in the User options tab along the top menu bar.
- Project-specific settings can be found in the Project options tab.

The options provided in the User options tab will apply every time we open Burp Suite. In contrast, the Project options will only apply to the current project. Given that we can't save projects in Burp Community, this means that our project options will reset every time we close Burp.

There are far too many options to cover them all, so let's just look at the available categories and highlight a few of the more few important settings. We will start with the User Options tab.

![Users Options](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-9.png)

The settings here apply globally (i.e. they control the Burp Suite application -- not just the project). That said, many of them can be overwritten in the project settings.

There are four main sub-sections of the User options tab:

- The options in the **Connections** sub-tab allow us to control how Burp makes connections to targets. For example, we can set a proxy for Burp Suite to connect through; this is very useful if we want to use Burp Suite through a network pivot.
- The **TLS** sub-tab allows us to enable and disable various TLS (Transport Layer Security) options, as well as giving us a place to upload client certificates should a web app require us to use one for connections.
- An essential set of options: **Display** allows us to change how Burp Suite looks. The options here include things like changing the font and scale, as well as setting the theme for the framework (e.g. dark mode) and configuring various options to do with the rendering engine in Repeater (more on this later!).
- The **Misc** sub-tab contains a wide variety of settings, including the keybinding table (HotKeys), which allowing us to view and alter the keyboard shortcuts used by Burp Suite. Familiarising yourself with these settings would be advisable, as using the keybinds can speed up your workflow massively.

With these options, we can customise our Burp install to suit our individual preferences.

Let's move on to look at the project-specific configurations available in the Project options tab.

There are five sub-tabs here:

- **Connections** holds many of the same options as the equivalent section of the User options tab: these can be used to override the application-wide settings. For example, it is possible to set a proxy for just the project, overriding any proxy settings that you set in the User options tab. There are a few differences between this sub-tab and that of the User options, however. For example, the "Hostname Resolution" option (allowing you to map domains to IPs directly within Burp Suite) can be very handy -- as can the "Out-of-Scope Requests" settings, which enable us to determine whether Burp will send requests to anything you aren't explicitly targeting (more on this later!).

- The **HTTP** sub-tab defines how Burp handles various aspects of the HTTP protocol: for example, whether it follows redirects or how to handle unusual response codes.

- **TLS** allows us to override application-wide TLS options, as well as showing us a list of public server certificates for sites that we have visited.

- The **Sessions** tab provides us with options for handling sessions. It allows us to define how Burp obtains, saves, and uses session cookies that it receives from target sites. It also allows us to define macros which we can use to automate things such as logging into web applications (giving us an instant authenticated session, assuming we have valid credentials).

- There are fewer options in the **Misc** sub-tab than in the equivalent tab for the "User options" section. Many of the options here are also only available if you have access to Burp Pro (such as those configuring Collaborator). That said, there are a couple of options related to logging and the embedded browser (which we will look at in a couple of tasks) that are well worth perusing.

**_Answer the questions below_**

1. **Change the Burp Suite theme to dark mode**

- **_Ans: No Answer Needed._**

2. **In which Project options sub-tab can you find reference to a "Cookie jar"?**

- **_Ans: Sessions_**

3. **In which User options sub-tab can you change the Burp Suite update behaviour?**

- **_Ans: Misc_**

4. **What is the name of the section within the User options "Misc" sub-tab which allows you to change the Burp Suite keybindings?**

- **_Ans: Hotkeys_**

5. **If we have uploaded Client-Side TLS certificates in the User options tab, can we override these on a per-project basis (Aye/Nay)?**

- **_Ans: Aye_**

6. **There are many more configuration options available. Take the time to read through them.**

**In the next section, we will cover the Burp Proxy -- a much more hands-on aspect of the room.**

- **_Ans: No Answer Needed._**

---

### Task 8: Proxy Introduction to the Burp Proxy

The Burp Proxy is the most fundamental (and most important!) of the tools available in Burp Suite. It allows us to capture requests and responses between ourselves and our target. These can then be manipulated or sent to other tools for further processing before being allowed to continue to their destination.

For example, if we make a request to `https://tryhackme.com` through the Burp Proxy, our request will be captured and won't be allowed to continue to the TryHackMe servers until we explicitly allow it through. We can choose to do the same with the response from the server, although this isn't active by default. This ability to intercept requests ultimately means that we can take complete control over our web traffic -- an invaluable ability when it comes to testing web applications.

There are a few configurations we need to make before we can use the proxy, but let's start by looking at the interface.

**Note:** _You do not need to follow along with this task -- just read the information and understand what the Proxy is used for._

When we first open the Proxy tab, Burp gives us a bunch of useful information and background reading. This information is well worth reading through; however, the real magic happens after we capture a request:

![Proxy Tab](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-10.png)

With the proxy active, a request was made to the TryHackMe website. At this point, the browser making the request will hang, and the request will appear in the Proxy tab giving us the view shown in the screenshot above. We can then choose to forward or drop the request (potentially after editing it). We can also do various other things here, such as sending the request to one of the other Burp modules, copying it as a cURL command, saving it to a file, and many others.

When we have finished working with the Proxy, we can click the "Intercept is on" button to disable the Intercept, which will allow requests to pass through the proxy without being stopped.

Burp Suite will still (by default) be logging requests made through the proxy when the intercept is off. This can be very useful for going back and analysing prior requests, even if we didn't specifically capture them when they were made.

Burp will also capture and log WebSocket communication, which, again, can be exceedingly helpful when analysing a web app.

The logs can be viewed by going to the "HTTP history" and "WebSockets history" sub-tabs:

![HTTP Proxy Tab](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-11.png)

It is worth noting that any requests captured here can be sent to other tools in the framework by right-clicking them and choosing "Send to...". For example, we could take a previous HTTP request that has already been proxied to the target and send it to Repeater.

Finally, there are also Proxy specific options, which we can view in the "Options" sub-tab.

These options give us a lot of control over how the proxy operates, so it is an excellent idea to familiarise yourself with these.

For example, the proxy will not intercept server responses by default unless we explicitly ask it to on a per-request basis. We can override the default setting by selecting the "Intercept responses based on the following rules" checkbox and picking one or more rules. The "`Or` `Request` `Was Intercepted`" rule is good for catching responses to all requests that were intercepted by the proxy:

![Intercept Server Response](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-12.png)

The "`And` `URL` `Is in target scope`" is another very good default rule; we will look at scoping later in this room.

You can make your own rules for most of the Proxy options, so this is one section where looking around and experimenting will serve you very well indeed!

Another particularly useful section of this sub-tab is the "Match and Replace" section; this allows you to perform regexes on incoming and outgoing requests. For example, you can automatically change your user agent to emulate a different web browser in outgoing requests or remove all cookies being set in incoming requests. Again, you are free to make your own rules here.

**_Answer the questions below_**

1. **Which button would we choose to send an intercepted request to the target in Burp Proxy?**

- **_Ans: Forward_**

2. **[Research] What is the default keybind for this?**

_**Note: Assume you are using Windows or Linux (i.e. swap Cmd for Ctrl).**_

- **_Ans: ctrl+F_**

---

### Task 9: Proxy Connecting through the Proxy (FoxyProxy)

You've seen the theory; now it's time to start using the proxy for yourself.

There are two ways to proxy our traffic through Burp Suite.

1. We could use the embedded browser (we will cover this in a later task).
2. We can configure our local web browser to proxy our traffic through Burp; this is more common and so will be the focus of this task.

The Burp Proxy works by opening a web interface on `127.0.0.1:8080` (by default). As implied by the fact that this is a "proxy", we need to redirect all of our browser traffic through this port before we can start intercepting it with Burp. We can do this by altering our browser settings or, more commonly, by using a Firefox browser extension called [FoxyProxy](https://getfoxyproxy.org/). FoxyProxy allows us to save proxy profiles, meaning we can quickly and easily switch to our "Burp Suite" profile in a matter of clicks, then disable the proxy just as easily.

**Note:** _All instructions will be given with Firefox in mind, as this is the default browser for both Kali Linux and the TryHackMe AttackBox. If you are using another browser locally then you are advised to use the AttackBox, or you may otherwise need to find alternative methods to those presented in this task. If you can't get the proxy working in your local browser and do not want to use the AttackBox, then you may wish to skip ahead to the Burp Suite Browser task._

There are two versions of FoxyProxy: Basic and Standard. Both versions allow you to change your proxy settings on the fly; however, FoxyProxy Standard gives you a lot more control over what traffic gets sent through the proxy. For example, it will allow you to set pattern matching rules to determine whether a request should be proxied or not: this is more complicated than the simple proxy offered by FoxyProxy basic.

The basic edition is more than adequate for our usage. It is pre-installed and configured in the Firefox browser of the AttackBox, so if you are using the AttackBox, please feel free to skip ahead to the last section of this task.

If you are using your own machine, you can download FoxyProxy Basic [here](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-basic/).

Once installed, a button should appear at the top right of the screen which allows you to access your proxy configurations:

![FoxyProxy](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-13.png)

There are no default configurations, so let's click on the "Options" button to create our Burp Proxy config.

This will open a new browser tab with the FoxyProxy options page:

![FoxyProxy Options](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-14.png)

Click on the "Add" button and fill in the following values:

1. Title: `Burp` (or anything else you prefer)
2. Proxy IP: `127.0.0.1`
3. Port: `8080`

![Add Proxy](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-15.png)

Now click "Save".

When you click on the FoxyProxy icon at the top of the screen, you will see that that there is a configuration available for Burp:

![Foxy Proxy](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-16.png)

If we click on the "Burp" config, our browser will start directing all of our traffic through 127.0.0.1:8080. Be warned: if Burp Suite is not running, your browser will not be able to make any requests when this config is activated!

Activate this config now -- the icon in the menu should change to indicate that we have a proxy running:

![Foxy Proxy Icon](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-17.png)

Next, switch over to Burp Suite and make sure the Intercept is On:

![Intercept The Request](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-18.png)

Now, try accessing the homepage for `http://MACHINE_IP/` in Firefox. Your browser should hang, and your proxy will populate with the request headers.

Congratulations, you just intercepted your first request!

From here, you can choose to forward or drop the request. Alternatively, you could send it to another tool or perform any number of other actions by right-clicking on the request and selecting an option from the right-click menu.

**_Remember:_** _Whilst you are connected to the proxy and have the Proxy Intercept switched on, your browser will hang whenever you make a request. A very common mistake when you are learning to use Burp Suite (and indeed, later on!) is to accidentally leave the intercept switched on and ergo be unable to make any web requests through your browser. If your browser is hanging and you don't know why: check your proxy!_

**_Answer the questions below_**

1. **Read through the options in the right-click menu.**

**There is one particularly useful option that allows you to intercept and modify the response to your request.**

**What is this option?**

**Note: The option is in a dropdown sub-menu.**

- **_Ans: Response to this request_**

2. **[Bonus Question -- Optional] Try installing FoxyProxy standard and have a look at the pattern matching features.**

- **_Ans: No Answer Needed._**

---

### Task 10: Proxy Proxying HTTPS

Note: The AttackBox is already configured to solve the problem posed in this task. If you are using the AttackBox and don't wish to read through the information here, you can skip to the next task.

Great, so we can intercept HTTP traffic -- what's next?

Unfortunately, there's a problem. What happens if we navigate to a site with TLS enabled? For example, `https://google.com/:`

![HTTPS Proxy](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-19.png)

We get an error.

Specifically, Firefox is telling us that the Portswigger Certificate Authority (CA) isn't authorised to secure the connection.

Fortunately, Burp offers us an easy way around this. We need to get Firefox to trust connections secured by Portswigger certs, so we will manually add the CA certificate to our list of trusted certificate authorities.

First, with the proxy activated head to http://burp/cert; this will download a file called `cacert.der` -- save it somewhere on your machine.

Next, type `about:preferences` into your Firefox search bar and press enter; this takes us to the FireFox settings page. Search the page for "certificates" and we find the option to "View Certificates":

![Burp Certificate](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-20.png)

Clicking the "View Certificates" button allows us to see all of our trusted CA certificates. We can register a new certificate for Portswigger by pressing "Import" and selecting the file that we just downloaded.

In the menu that pops up, select "Trust this CA to identify websites", then click Ok:

![CA Certificate](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-21.png)

We should now be free to visit any TLS enabled sites that we wish!

The following video shows the full import process:

![Burp Certificate](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-22.gif)

**_Answer the questions below_**

1. **If you are not using the AttackBox, configure Firefox (or your browser of choice) to accept the Portswigger CA certificate for TLS communication through the Burp Proxy.**

- **_Ans: No Answer Needed._**

---

### Task 11: Proxy The Burp Suite Browser

If the last few tasks seemed overly complex, rest assured, this topic will be a lot simpler.

In addition to giving us the option to modify our regular web browser to work with the proxy, Burp Suite also includes a built-in Chromium browser that is pre-configured to use the proxy without any of the modifications we just had to do.

Whilst this may seem ideal, it is not as commonly used as the process detailed in the previous few tasks. People tend to stick with their own browser as it gives them a lot more customisability; however, both are perfectly valid choices.

We can start the Burp Browser with the "Open Browser" button in the proxy tab:

![Burp Suite Browser](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-23.png)

A Chromium window will now pop up. Any requests we make in this will go through the proxy.

**_Note:_** _There are many settings to do with the Burp Browser in the Project options and User options tabs -- make sure to go look at them!_

If we are running on Linux as the root user (as we are with the AttackBox), Burp Suite is unable to create a sandbox environment to start the Burp Browser in, causing it to throw an error and die:

![Burp Browser Error](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-24.png)

There are two simple solutions to this:

- **The smart option:** We could create a new user and run Burp Suite under a low privilege account.
- **The easy option:** We could go to `Project options -> Misc -> Embedded Browser` and check the `Allow the embedded browser to run without a sandbox` option. Checking this option will allow the browser to start, but be aware that it is disabled by default for security reasons: if we get compromised using the browser, then an attacker will have access to our entire machine. On the training environment of the AttackBox this is unlikely (and isn't a huge issue even if it does happen), but keep it in mind if you try this on a local installation of Burp Suite.

Be aware that you will need to do this if using the embedded browser on the AttackBox.

**_Answer the questions below_**

1. **Using the in-built browser, make a request to http://MACHINE_IP/ and capture it in the proxy.**

- **_No Answer Needed._**

---

### Task 12 Proxy Scoping and Targeting

Finally, we come to one of the most important parts of using the Burp Proxy: Scoping.

It can get extremely tedious having Burp capturing all of our traffic. When it logs everything (including traffic to sites we aren't targeting), it muddies up logs we may later wish to send to clients. In short, allowing Burp to capture everything can quickly become a massive pain.

What's the solution? Scoping.

Setting a scope for the project allows us to define what gets proxied and logged. We can restrict Burp Suite to only target the web application(s) that we want to test. The easiest way to do this is by switching over to the "Target" tab, right-clicking our target from our list on the left, then choosing "Add To Scope". Burp will then ask us whether we want to stop logging anything which isn't in scope -- most of the time we want to choose "yes" here.

![Project Scoping](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-25.gif)

We can now check our scope by switching to the "Scope" sub-tab (as shown in the GIF above).

The Scope sub-tab allows us to control what we are targeting by either Including or Excluding domains / IPs. This is a very powerful section, so it's well worth taking the time to get accustomed to using it.
We just chose to disable logging for out of scope traffic, but the proxy will still be intercepting everything. To turn this off, we need to go into the Proxy Options sub-tab and select "`And URL Is in target scope`" from the Intercept Client Requests section:

![Project Scoping](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-26.png)

With this option selected, the proxy will completely ignore anything that isn't in the scope, vastly cleaning up the traffic coming through Burp.

**_Answer the questions below_**

1. **Add http://MACHINE_IP/ to your scope and change the Proxy settings to only intercept traffic to in-scope targets.**

**See the difference between the amount of traffic getting caught by the proxy before and after limiting the scope.**

- **_No Answer Needed._**

---

### Task 13: Proxy Site Map and Issue Definitions

Control of the scope may be the most useful aspect of the Target tab, but it's by no means the only use for this section of Burp.

There are three sub-tabs under Target:

- **Site map** allows us to map out the apps we are targeting in a tree structure. Every page that we visit will show up here, allowing us to automatically generate a site map for the target simply by browsing around the web app. Burp Pro would also allow us to spider the targets automatically (i.e. look through every page for links and use them to map out as much of the site as-is publicly accessible using the links between pages); however, with Burp Community, we can still use this to accumulate data whilst we perform our initial enumeration steps.
  The Site map can be especially useful if we want to map out an API, as whenever we visit a page, any API endpoints that the page retrieves data from whilst loading will show up here.
- **Scope:** We have already seen the Scope sub-tab -- it allows us to control Burp's target scope for the project.
- **Issue Definitions:** Whilst we don't have access to the Burp Suite vulnerability scanner in Burp Community, we do still have access to a list of all the vulnerabilities it looks for. The Issue Definitions section gives us a huge list of web vulnerabilities (complete with descriptions and references) which we can draw from should we need citations for a report or help describing a vulnerability.

**_Answer the questions below_**

1. **Take a look around the site on http://MACHINE_IP/ -- we will be using this a lot throughout the module. Visit every page linked to from the homepage, then check your sitemap -- one endpoint should stand out as being very unusual!**

**Visit this in your browser (or use the "Response" section of the site map entry for that endpoint)**

**What is the flag you receive?**

- **_THM{NmNlZTliNGE1MWU1ZTQzMzgzNmFiNWVk}_**

2. **Look through the Issue Definitions list.**

**What is the typical severity of a Vulnerable JavaScript dependency?**

- **_Ans: Low_**

---

### Task 14: Practical Example Attack

Having looked at how to set up and configure our proxy, let's go through a simplified real-world example.

We will start by taking a look at the support form at `http://MACHINE_IP/ticket/:`

![HTML Form](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-27.png)

In a real-world web app pentest, we would test this for a variety of things: one of which would be Cross-Site Scripting (or XSS). If you have not yet encountered XSS, it can be thought of as injecting a client-side script (usually in Javascript) into a webpage in such a way that it executes. There are various kinds of XSS -- the type that we are using here is referred to as "Reflected" XSS as it only affects the person making the web request.

Let's begin.

**_Answer the questions below_**

1. **Try typing: `<script>alert("Succ3ssful XSS")</script>`, into the "Contact Email" field. You should find that there is a client-side filter in place which prevents you from adding any special characters that aren't allowed in email addresses:**

![HTML Form](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-28.gif)

- **_No Answer Needed._**

2. **Fortunately for us, client-side filters are absurdly easy to bypass. There are a variety of ways we could disable the script or just prevent it from loading in the first place.**

**Let's focus on simply bypassing the filter for now.**

**First, make sure that your Burp Proxy is active and that the intercept is on.**

- **_No Answer Needed._**

3. **Now, enter some legitimate data into the support form. For example: "pentester@example.thm" as an email address, and "Test Attack" as a query.**

**Submit the form -- the request should be intercepted by the proxy.**

- **_No Answer Needed._**

4. **With the request captured in the proxy, we can now change the email field to be our very simple payload from above: `<script>alert("Succ3ssful XSS")</script>`. After pasting in the payload, we need to select it, then URL encode it with the Ctrl + U shortcut to make it safe to send. This process is shown in the GIF below:**

**GIF demonstrating the explained process of intercepting and URL encoding the pasted payload**

![Proxy](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-29.gif)

**Finally, press the "Forward" button to send the request.**

**You should find that you get an alert box from the site indicating a successful XSS attack!**

![XSS Attack](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Burp-Suite-The-Basics/Picture-30.png)

- **_No Answer Needed._**

5. **Congratulations, you bypassed the filter!**

**Don't expect it to be quite so easy in real life, but this should hopefully give you an idea of the kind of situation in which Burp Proxy can be useful.**

- **_No Answer Needed._**

---

### Task 15: Conclusion Room Conclusion

We have now reached the end of the Burp Basics room.

This room has hopefully given you a good grasp of the Burp Suite interface and configuration options, as well as giving you a working knowledge of the Burp Proxy.

You are advised to experiment with these foundations until you are completely comfortable with them. Burp Suite is an invaluable tool in a web or mobile application pentester's arsenal. We will be building on these skills in the next room of the module covering Burp Suite Repeater.

**_Answer the questions below_**

1. **I understand the fundamentals of using Burp Suite!**

- **_Ans: No Answer Needed_**

---

### CREDITS: Created by [tryhackme](https://tryhackme.com/p/tryhackme) and [MuirlandOracle](https://tryhackme.com/p/MuirlandOracle)

---
