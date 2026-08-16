---
title: Bandit 30 -> 31

---

# Task
>There is a git repository at ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo via the port 2220. The password for the user bandit30-git is the same as for the user bandit30.

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit30\
Password: jq9Dfg2rXsfYsWMgFuKlXhphjdH7USgX

# Solution

Reading the `README.md` file only provides:

![image](/pngs/bandit30_31_1.png)

Upon further checking there were no other logs nor branches to be found.

So I checked if there's any tag:

![image](/pngs/bandit30_31_2.png)

Showing the tag returns the password:

![image](/pngs/bandit30_31_3.png)


# Password
```
82NkymblpGBYmIXG6ZQ8YldBYstHpfUf
```