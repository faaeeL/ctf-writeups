---
title: Bandit 17 -> 18

---

# Task
>There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit17
Password: private ssh key

# Solution

Using the command `diff` we can compare the differences between the old and new files

![image](/pngs/tldr_diff.png)

```
bandit17@bandit:~$ diff passwords.old passwords.new                                     
42c42
< icUh23IUytZLIYhcCaXL18agiSIqymBc
---
> OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

# Password

```
OQxXZjELndr90zuhOTDYBEomI0SZITXI
```