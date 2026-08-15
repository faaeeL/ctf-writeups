---
title: Bandit 18 -> 19

---

# Task
>The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit18\
Password: OQxXZjELndr90zuhOTDYBEomI0SZITXI

# Solution

Since we are immdiately logged out upon logging in with SSH we can add `cat readme` at the end at the command to read the file upon logging in.

![image](/pngs/bandit18.png)

# Password
```
KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI
```