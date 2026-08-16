---
title: Bandit 31 -> 32

---

# Task
>There is a git repository at ssh://bandit31-git@bandit.labs.overthewire.org/home/bandit31-git/repo via the port 2220. The password for the user bandit31-git is the same as for the user bandit31.

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit31\
Password: 82NkymblpGBYmIXG6ZQ8YldBYstHpfUf

# Solution

Cloning and checking out files:

![image](/pngs/bandit31_32_1.png)

After doing what the files tell me to do:

![image](/pngs/bandit31_32_2.png)

I saw that I didn't commit anything although I added the file.

Checking the `.gitignore` file I can see that it ignores `.txt` file:

```shell
cat .gitignore
*.txt
```

So I should add the flag `-f` to force adding it:

![image](/pngs/bandit31_32_3.png)


# Password
```
pWuj5jBQ6IgV0NXwiH6g1pXRF8S1YvbT
```
