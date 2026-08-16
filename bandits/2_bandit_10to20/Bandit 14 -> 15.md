
# Task
> The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit14\
Password: aaWecNkG4FhxJQxz07uiwzVP6bJiYS65

# Solution

Checking out what telnet do:

![image](/pngs/tldr_telnet.png)

Trying out the command:

```
bandit14@bandit:~$ telnet localhost 30000
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
Correct!
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7

Connection closed by foreign host.
```

# Password
```
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

