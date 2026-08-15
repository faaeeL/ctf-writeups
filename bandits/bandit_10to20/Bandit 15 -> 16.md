---
title: Bandit 15 -> 16

---

# Task
>The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.
Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

Server: bandit.labs.overthewire.org\
Port: 2220\
Username: bandit15\
Password: pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7

# Solution

Using the command `openssl s_client localhost:30001` to connect:

```
bandit15@bandit:~$ openssl s_client localhost:30001
Connecting to 127.0.0.1
CONNECTED(00000003)
...
read R BLOCK
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
Correct!
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V

closed
```

# Password
```
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```