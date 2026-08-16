---
title: Bandit 28 -> 29

---

# Task
>There is a git repository at ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo via the port 2220. The password for the user bandit28-git is the same as for the user bandit28.

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit28\
Password: y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ

# Solution

Cloning the repo to my machine I have the file `README.md`:

![image](/pngs/bandit28_29_1.png)

Reading the file doesn't give us the password to the next level but instead:

![image](/pngs/bandit28_29_2.png)

We can use `git log` to see the past commits to this repo:

![image](/pngs/bandit28_29_3.png)

The commit with the comment `fix info leak` seems promising so we can use `git show` to see what were the changes:

![image](/pngs/bandit28_29_4.png)


# Password
```
Em7eGtqaMySwNFjCpwzzHhLhospOcdt0
```