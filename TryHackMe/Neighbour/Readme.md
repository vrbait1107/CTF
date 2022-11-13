## Neighbour

#### Check out our new cloud service, Authentication Anywhere. Can you find other user's secrets?

---

**Task 1: Neighbour**

Check out our new cloud service, Authentication Anywhere -- log in from anywhere you would like! Users can enter their username and password, for a totally secure login process! You definitely wouldn't be able to find any secrets that other people have in their profile, right?022 -- 1 IP address (1 host up) scanned in 9.51 seconds

Access this challenge by deploying both the vulnerable machine by pressing the green "Start Machine" button located within this task, and the TryHackMe AttackBox by pressing the  "Start AttackBox" button located at the top-right of the page.

Navigate to the following URL using the AttackBox: http://MACHINE_IP


Check out similar content on TryHackMe:

- IDOR

**Steps to Solve**

1. Visit the Website, We can see there is login option and indicate that to view view page source.

![Login Page](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Neighbour/Picture-1.png)

2. View page source indicates that use username and password as guest.

![View Page Source](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Neighbour/Picture-2.jpg)

3. Using username and password of guest, we will redirect to test user.

![Test User Account](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Neighbour/Picture-3.jpg)

4. Rooms is belong to IDOR issue, We can clear see test in url just change to admin and we will get the flag.

![Admin User Account and Flag](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Neighbour/Picture-4.png)

***Answer the questions below***

1. **Uncover the flag!**
- **flag{66be95c`*****************`0c7af1f}**

---
