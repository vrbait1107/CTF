## [Day 4] Web Exploitation Santa's Running Behind

### Story

McSysAdmin managed to reset everyone's access except Santa's! Santa's expected some urgent travel itinerary for his route over Christmas. Rumour has it that Santa never followed the password security recommendations. Can you use bruteforcing to help him access his accounts?

### Learning Objectives

In today’s task, we’re going to learn the following.

1. Understanding authentication and where it is used
2. Understanding what fuzzing is
3. Understanding what Burp Suite is and how we can use it for fuzzing a login form to gain access
4. Apply this knowledge to retrieve Santa’s travel itinerary

### What is authentication, and where is it Used?

Authentication is the process of verifying a user’s identity, establishing that they are who they say they are. Authentication can be proven using a variety of authentication means, including:

1. A known set of credentials to the server and user such as a username and password
2. Token authentication (these are unique pieces of encrypted text)
3. Biometric authentication (fingerprints, retina data, etc.)

Authentication is often used interchangeably with authorisation, but it is very different. Authorisation is a term for the rules defining what an authenticated user can and cannot access. For example, a standard, the **authenticated** user will only be allowed access to some aspects of a website. An authenticated administrator will be able to access the entire thing – their level of authorisation determines this.

Authentication is used when there is a necessity to know who is accessing pieces of data or information to create accountability – protecting the Confidentiality element of the CIA triad. If you wish to learn more about this, I recommend checking out the Principles of Security room on TryHackMe. You can find examples of authentication in the real world, for example, a badge or key-card to access restricted places within a building.

### What is Fuzzing?

Put simply, fuzzing is an automated means of testing an element of a web application until the application gives a vulnerability or valuable information. When we are fuzzing, we provide information as we would typically when interacting with it, just at a much faster rate. This means that we can use extensive lists known as wordlists to test a web application’s response to various information.

For example, rather than testing a login form for a valid set of credentials one-by-one (which is exceptionally time-consuming), we can use a tool for fuzzing this login form to test hundreds of credentials at a much faster rate and more reliably.

### Fuzzing with Burp Suite

Please note that this task presumes that you are using the TryHackMe AttackBox. The AttackBox has the necessary software, tools and wordlists installed for you to complete today’s task – so it is highly recommended that you use it (to start it, scroll to the top of this page and click the blue "Start AttackBox" button, then follow the steps below).

1. Let’s launch FireFox by navigating to “Applications -> Internet-> Firefox”

![Firefox Browser](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-1.png "Firefox Browser")

2. Navigate to the login form in the web browser using the vulnerable IP address (http://MACHINE_IP) (note that the IP address in the screenshots is only an example, you will need to replace this with the MACHINE_IP)

![URL](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-2.png "URL")

3. Let’s launch Burp Suite by navigating to “Applications -> Other -> Burp Suite"

![Burp Suite](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-3.png "Burp Suite")

4. Navigate to the "Proxy" tab:

![Burp Suite Proxy Tab](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-4.png "Burp Suite Proxy Tab")

5. And press "Intercept On" in "Proxy -> Intercept"

6. Now we will need to return to our Firefox Browser and enable the FoxyProxy extension in Firefox. You can do this by pressing the “FoxyProxy” extension and pressing “Burp” like so:

![Foxy Proxy](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-5.png "Foxy Proxy")

7. Submit some dummy data on the login form, such as below. Please note that the web browser will hang:

![Login Page](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-6.png "Login Page")

8. We will need to return to Burp Suite, where we will see some data has now been returned to us. Right-click the window containing the data and press “Send to Intruder”

![Intruder Tab](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-7.png "Intruder Tab")

9. Navigate to the “Intruder” tab and select the following:

10. Click the “Positions” tab and clear the pre-selected positions by pressing "Clear $"

- Add the value of the "username" parameter as the first position, sometimes we will already know the username, other times we will not. We can tell Burp to use a wordlist of usernames for this position as well. However, as the username is already known (i.e. cmnatic), we are just brute-forcing the password. (this can be done by highlighting the password parameter and clicking “Add $”)

- Add the “password” value as the position (i.e. password123) (this can be done by highlighting the value in the password parameter and clicking “Add $”)

- Select “Cluster Bomb” in the Attack type in the dropdown menu.

- We will now need to provide some values for Burp Suite to fuzz the login form with passwords. We can provide a list manually, or we can provide a wordlist. I will be providing a wordlist.

![Wordlists](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-8.png "Wordlists")

11. Now after selecting our wordlist, we can see that some passwords have filled the “Payload Options” window:

![Payload Options](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-9.png "Payload Options")

12. Now let’s press the “Start Attack” button, this will begin fuzzing the login form. Look at the results and sort by “Length”. Unsuccessful passwords will return a certain length, and successful passwords will return another length. You will need to examine the results with different lengths to determine the correct password in today’s task.

Navigate to the vulnerable login form at http://MACHINE_IP/ and apply the material for today's task to login to Santa's itinerary, using the username as "santa" and the password list located at `/root/Rooms/AoC3/Day4/passwords.txt` on the TryHackMe AttackBox (or download it from here for your payload.

### Additional Resources

If you are interested in learning more about Burp Suite, check out the Burp Suite module on TryHackMe.

---

**_Answer the questions below_**

1. **Access the login form at http://MACHINE_IP**

- **_No Answer Needed_**

2. **Configure Burp Suite & Firefox, submit some dummy credentials and intercept the request. Use intruder to attack the login form.**

- **_No Answer Needed_**

3. **What valid password can you use to access the "santa" account?**

- **_cookie_**

**Login Page**

![Login Page](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-10.png "Login Page")

**Capture Request**

![Intercept Request](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-11.png "Intercept Request")

**Payloads**

![Payload Options](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-12.png "Payload Options")

**Intruder**

![Payload Options](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-13.png "Payload Options")

**Flag**

![Payload Options](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Advent-of-cyber-3/Day-4/Picture-14.png "Payload Options")

4. **What is the flag in Santa's itinerary?**

- **_THM{SANTA_DELIVERS}_**

---
