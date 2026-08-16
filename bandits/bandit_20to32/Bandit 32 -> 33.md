---
title: Task

---

# Task
>After all this git stuff, it’s time for another escape. Good luck!

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit32\
Password: pWuj5jBQ6IgV0NXwiH6g1pXRF8S1YvbT

# Solution

Upon entering the shell and testing out command, I can see that any command I input is made uppercase.

```shell
>> ls
sh: 1: LS: Permission denied
```

So in order to break out of this I need to use the built-in shell variable that is `$0`.

Since it consist of a special character and a number it wouldn't be affected by the uppercase shell.

And the `$0` is a special shell variable that expands to the name of the current shell interpreter or the path of the executing script so it effectively starts a fresh shell.

![image](/pngs/bandit32_33.png)

Checking the files I can see that it is ran under user bandit33 so I can just read the password file:

```shell
$ cat /etc/bandit_pass/bandit33
u4P2CyPOwPGLe94RdD9Uo2FxFwvnFswM
```

# Password
```
u4P2CyPOwPGLe94RdD9Uo2FxFwvnFswM
```

# Notes
`$0` is a special shell variable that expands to the name of the current shell interpreter or the path of the executing script.