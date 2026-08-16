---
title: Bandit 27 -> 28

---

# Task
>There is a git repository at ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo via the port 2220. The password for the user bandit27-git is the same as for the user bandit27.

>From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.



Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit27\
Password: STJLJBRRphMxKB392CT4iOr5CbzPU9ER

# Solution

For this level we only need to do the command

```
git clone ssh://bandit27git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```

After that we can read the files in the repo:

![image](/pngs/bandit27_28.png)


# Password
```
y8Yd2ssKcpHpud7UvOSOxwamRMzIGIeQ
```