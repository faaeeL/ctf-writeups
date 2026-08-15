---
title: Bandit 19 -> 20

---

# Task
>To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit19\
Password: KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI

# Solution

According to the wikipedia page the flag `setuid` allow users to run an executable with the file system permissions of the executable's owner or group.

![image](/pngs/bandit19.png)


![image](/pngs/bandit19_2)

So we can run this executable along with the command `cat /etc/bandit_pass/bandit20` to read the password file for bandit20

```
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
```

# Password
```
4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
```