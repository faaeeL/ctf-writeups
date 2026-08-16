---
title: Bandit 29 -> 30

---

# Task
>There is a git repository at ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo via the port 2220. The password for the user bandit29-git is the same as for the user bandit29.



Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit29\
Password: b607fba0c867d0bbdf4b4a5e62cd04b79c8fea83

# Solution

Cloning the repo and checking the `README.md` file:

![image](/pngs/bandit29_30_1.png)

There might be other branches in this repo so we can use the command `git branch -a` to list all the branches:

![image](/pngs/bandit29_30_2.png)

And then we can check out other branches using `git checkout`:

![image](/pngs/bandit29_30_3.png)


# Password
```
jq9Dfg2rXsfYsWMgFuKlXhphjdH7USgX
```