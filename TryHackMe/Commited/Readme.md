# Committed

#### One of our developers accidentally committed some sensitive code to our GitHub repository. Well, at least, that is what they told us...


### Task 1 : Commited 

Oh no, not again! One of our developers accidentally committed some sensitive code to our GitHub repository. Well, at least, that is what they told us... the problem is, we don't remember what or where! Can you track down what we accidentally committed?


Access this challenge by deploying the machine attached to this task by pressing the green "Start Machine" button. You will need to use the in-browser view to complete this room. Don't see anything? Press the "Show Split Screen" button at the top of the page.

The files you need are located in /home/ubuntu/commited on the VM attached to this task.


**Steps**

- Unzip the commited zip.
- Run git status command to check status of repository.
- then run git branch to check branches of repository.
- there are to branches of respository one is master/main which default branch of repository.
- check one by one branch 
- use command git log (commit hash) to view what commited.
- we can use git branch to check all git branch 
- git checkout <branch name> to switch in branch.

- Check Master Branch Git Logs 
![Master Branch Logs](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Commited/Picture-1.png)

- dbint Branch Git Logs
![Master Branch Logs](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Commited/Picture-2.png)

- Not Found in dbint Branch
![Note in dbint Branch](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Commited/Picture-3.png)

- Which means there is hardcoded password and flag in the code.
- Check manually logs

- We got password and flag. ( Using Grep Command)

![Flag](https://github.com/vrbait1107/CTF_WRITEUPS/blob/main/TryHackMe/images/Commited/Picture-5.png)

**_Answer the questions below_**

1. **Discover the flag in the repository!**

- **_flag{a489`***********************`da17b}_**