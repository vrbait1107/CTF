# Confidential

#### We got our hands on a confidential case file from some self-declared "black hat hackers"... it looks like they have a secret invite code.


### Task 1 : Confidential 

We got our hands on a confidential case file from some self-declared "black hat hackers"... it looks like they have a secret invite code available within a QR code, but it's covered by some image in this PDF! If we want to thwart whatever it is they are planning, we need your help to uncover what that QR code says!


Access this challenge by deploying the machine attached to this task by pressing the green "Start Machine" button. This machine shows in Split View in your browser, if it doesn't automatically display you may need to click "Show Split View" in the top right.

The file you need is located in /home/ubuntu/confidential on the VM.


Check out similar content on TryHackMe:

- Intro to digital forensics

**Steps**

- Start the VM
- There is one pdf.

![PDF](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Confidential/Picture-1.png)
- There is one tool, pdfiamges we extract pdf images from that.
- run command `pdfimages --help` we can see help section.
![pdfimages help](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Confidential/Picture-2.png)
- Run command `pdfimages -png Repdf.pdf ext` to extract image in png format.
![QR Code](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Confidential/Picture-3.png)
- We have now png images of QR Code.
![QR Code](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Confidential/Picture-4.png)
- Just crop QR code to find flag.
![Cropeed QR Code](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Confidential/Picture-5.png)
- Flag
![Flag](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Confidential/Picture-6.png)



**_Answer the questions below_**

1. **Uncover and scan the QR code to retrieve the flag!**

- **_flag{e08e`************************`7a8d}_**