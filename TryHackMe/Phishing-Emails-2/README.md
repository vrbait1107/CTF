## Phishing Emails 2

### Task 1: Introduction

Now that we covered the basics concerning emails in Phishing Emails 1, let's dive right into actual phishing email samples.

Each email sample showcased in this room will demonstrate different tactics used to make the phishing emails look legitimate. The more convincing the phishing email appears, the higher the chances the recipient will click on a malicious link, download and execute the malicious file, or even send the prince of some country a wire transfer.

**Warning:** The samples throughout this room contain information from actual spam and/or phishing emails. Proceed with caution if you attempt to interact with any IP, domain, attachment, etc.

---

**_Answer the questions below_**

1. **Read the above.**

- **_No Answer Needed_**

---

### Task 2 Cancel your PayPal order

The email sample in this task will highlight the following techniques:

- Spoofed email address
- URL shortening services
- HTML to impersonate a legitimate brand

Here are some quick observations about this email sample:

1. This is an unusual email recipient address. This is not the email address associated with the Yahoo account.
2. This mismatch should immediately stand out. The sender's details (service@paypal.com) don't match the sender's email address (gibberish@sultanbogor.com).
3. The subject line hints that you made a purchase or a transaction of some sort. If you don't recall this account, then it will grab your attention. This social engineering tactic is to prompt you to interact with the email with haste.

![Receipt](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-1.png "Receipt")

Now let's look at the contents of the email body.

**Email Body Text (Image 1):**

![Email Body](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-2.png "Email Body")

The second half of the same email body text (Image 2):

![Email Body](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-3.png "Email Body")

The email body compliments the sender information and subject line. The email was designed as a legitimate email from PayPal.

There aren't any attachments associated with this email. The only interactive element in this email is the **Cancel the order** button/link.

Let's investigate that further by reviewing the raw HTML source for the email...

**Email Hyperlinks:**

![Email HyperLinks](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-4.png "Email HyperLinks")

The link uses URL shortening services. It is not a good idea to click on the link if you don't know where the link is taking you.

Luckily, there are online tools that we can use to let us know the destination of a shortened URL.

![URL Shortner](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-5.png "URL Shortner")

Strange. This link redirects to google.com.

**Note:** Tools to expand shortened URLs will be discussed in the Phishing Emails 3 room.

---

**_Answer the questions below_**

1. **What phrase does the gibberish sender email start with?**

- **_noreply_**

---

### Task 3: Track your package

This email sample will highlight the following techniques:

1. Spoofed email address
2. Pixel tracking
3. Link manipulation

Here are some quick observations about this email sample:

- The email is tailored to appear that it's sent from a mail distribution center of some sort.
- The subject line adds to the pretense with a 'tracking number.'
- The link in the email body matches the subject line.

![Track Your Package](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-6.png "Track Your Package")


**Note:** In this email sample, Yahoo blocked the images from automatically loading. Any guesses as to why? 

Typically one can hover the cursor over a link to see where the link is pointing to, but in this sample, that technique won't work because Yahoo disabled links in the email.  We can look at the raw source code for the email and find out. 

**Email Hyperlinks:**

![Email Hyperlinks](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-7.png "Email Hyperlinks")

Here we see an image file, and it's explicitly called **Tracking.png**. These trackers send information back to the spammer's server. 

There are many reasons for spammers to embed tracking pixels (very small images) into their spam emails. To read more about this concept, refer to this post on The Verge here. 

Now we can understand why Yahoo automatically blocked the images in this email. Many email providers do the same. 

Back to the hyperlink, the link is pointing to a shady-looking domain. The only distribution center this domain can be associated with is malware, but further analysis is the only way to confirm that definitely. 

---

***Answer the questions below***

1. **What is the root domain for each URL? Defang the URL.**
- ***Ans- devret[.]xyz***

---

### Task 4: Select your email provider to view document 

This email sample will highlight the following techniques:

- **Urgency**
- **HTML to impersonate a legitimate brand**
- **Link manipulation**
- **Credential harvesting**
- **Poor grammar and/or typos**

Let's take a closer look...

![Email](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-8.png "Email")

Here are some quick observations about this email sample:

1. The email was sent on Thursday, July 15th, 2021.  
2. A sense of urgency is introduced in this email. Notice that the link to download the fax document expires on the same day.
3. There is an action to perform. In this case, a button to download the fax. 

![OneDrive](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-9.png "OneDrive")

The above image shows the victim is redirected to a page created to pass as OneDrive. Notice that the URL is not anything Microsoft-related. 

There are two more links for the victim to interact with. The victim has to click either button to obtain the fax document that is set to expire. 

![Adobe Document Cloud](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-10.png "Adobe Document Cloud")

The victim is directed to yet another site. This one was crafted to resemble Adobe. Again, notice the URL. It doesn't look like it's related to Adobe.

Also, notice the page title in the tab. It's called "Share Point Online", which is a Microsoft product.  There are a couple of grammatical errors as well. 

The victim has options to sign in with the email provider of their choice. 

![OutLook](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-11.png "OutLook")

Our victim chose to log in with Outlook because, per the instructions, "To read the document, please enter with the valid email credentials that this file was sent to."; the email was viewed in Outlook.

![OutLook](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-12.png "OutLook")

In this sample, we can tell that fake credentials were entered, but even if the victim would have entered valid credentials, the error message would be the same. This scenario happens because the victim is not really authenticating to an email provider. Instead, the credentials that were entered now reside on the criminal's server. The criminal's objective to harvest credentials has been met. 

Lastly, notice more grammatical errors. All this work they put into this, you would think they would run a spell check. 

This email sample was obtained from Any Run. If you wish to interact with the email and see the full analysis, refer to the link below.

---

***Answer the questions below***

1. **This email sample used the names of a few major companies, their products, and logos such as OneDrive and Adobe. What other company name was used in this phishing email?**
- ***Ans- Citrix***

---

### Task 5: Please update your payment details 

This email sample will highlight the following techniques:

1. Spoofed email address
2. Urgency
3. HTML to impersonate a legitimate brand
4. Poor grammar and/or typos
5. Attachments

Here are some quick observations about this email sample:

- This email is made to appear that it's from Netflix Billing, but the sender address is z99@musacombi.online. 
- Here is the element of urgency. The account was suspended, so the victim must act quickly. 
- There is more of this sense of urgency in the email body. 

![NetFlix](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-13.png "NetFlix")

Also, notice the different misspellings of the word Netflix. Not sure what was the purpose of that. 

Typically, you'll see this technique when it comes to typosquatting, but that wasn't the case here.

![Message](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-14.png "Message")

Ok, here is the meat and potatoes of this email. Apparently, the victim needs to open the attachment (PDF) to update their Netflix account.

![Update Payment](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-15.png "Update Payment")

Notice the phone number for 'Netflix'. At first glance, that is an unusual phone number to send to a US-based victim.

![Reset Password](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-16.png "Reset Password")

The attachment contains an embedded link titled 'Update Payment Account'. 

We'll look at this email attachment in closer detail in the upcoming Phishing Emails 3 room. 

---

***Answer the questions below***

1. **What should users do if they receive a suspicious email or text message claiming to be from Netflix?**
- ***Ans- forward the message to phishing@netflix.com***

---


### Task 6: Your recent purchase 

This email sample will highlight the following techniques:

- **Spoofed email address**
- **Recipient is BCCed**
- **Urgency**
- **Poor grammar and/or typos**
- **Attachments**

Here are some quick observations about this email sample:

- This email is made to appear that it's from Apple Support, but the sender's address is gibberish@sumpremed.com. 
- This email wasn't sent directly to the victim's inbox but rather BCCed (Blind Carbon Copy). The recipient email looks like another spoofed email to appear as a legitimate Apple email address. 
- Here is the element of urgency. Action is required on behalf of the victim. 

![Apple Support](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-17.png "Apple Support")

There are a few noticeable typos in both the sender and recipient email addresses: donoreply and payament.

This particular email doesn't necessarily have an email body. It's totally blank. The email simply contains an attachment.

![Word](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-18.png "Word")

This file extension you may not be familiar to you. A .DOT file is page layout template files associated with Microsoft Word. 

![Word](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-19.png "Word")

The above image shows what is contained within the attachment. You can see that the file contains a large image to resemble an App Store receipt. 

Notice the link contains certain keywords related to Apple: **apps and ios.**

---

***Answer the questions below***

1. **What does BCC mean?**
- ***Ans- Blind Carbon Copy***

2. **What technique was used to persuade the victim to not ignore the email and act swiftly?**
- ***Ans- Urgency***

---

### Task 7: DHL Express Courier Shipping notice 

This email sample will highlight the following techniques:

- **Spoofed email address**
- **HTML to impersonate a legitimate brand**
- **Attachments**

Here are some quick observations about this email sample:

- The sender's email doesn't match the company that is being impersonated, which in this case is DHL.
- The subject line gives the impression that there is a package DHL will ship for you.
- The HTML in the email body was designed to look like it was sent from DHL. 

![DHL](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-20.png "DHL")

Looking at the source code for the email, the link to view the email as a web page doesn't contain an actual destination URL. 


![DHL](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-21.png "DHL")

The only element the victim can interact with in this email is the email attachment, which, in this case is an Excel document. 

![DHL](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-22.png "DHL")

![xlxs](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-23.png "xlxs")

The image below shows what is contained within the attachment.

![Attachment](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-24.png "Attachment")

The attachment runs a payload that throws an error. 

![Attachment](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Phishing-Emails-2/Picture-25.png "Attachment")

---

***Answer the questions below***

1. **What is the name of the executable that the Excel attachment attempts to run?**
- ***Ans- regasms.exe***

---

### Task 8 Conclusion

In this room, we looked at various phishing samples. 

Some of the samples shared similar techniques whereas, others introduced a new tactic for you to see and learn from. 

Understanding how to detect phishing emails takes awareness training.

Visit the resources below to acquaint yourself with other signs to look out for in phishing emails. 

Additional Resources:

- https://www.knowbe4.com/phishing
- https://www.itgovernance.co.uk/blog/5-ways-to-detect-a-phishing-email
- https://cheapsslsecurity.com/blog/10-phishing-email-examples-you-need-to-see/
- https://phishingquiz.withgoogle.com

The next room in this module: Phishing Emails 3

---

**_Answer the questions below_**

1. **Read the above.**

- **_No Answer Needed_**

---

