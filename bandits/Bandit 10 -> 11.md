# Task
#### The password for the next level is stored in the file data.txt, which contains base64 encoded data.

Server: bandit.labs.overthewire.org
Port: 2220
Username: bandit10
Password: B0s2khmbT9u0geKuOoVGW3JZKhndE3BG

# Solution

Navigating through files:

```
bandit10@bandit:~$ ls -la
total 24
drwxr-xr-x   2 root     root     4096 Jun 24 14:58 .
drwxr-xr-x 150 root     root     4096 Jun 24 15:02 ..
-rw-r--r--   1 root     root      220 Feb 13  2026 .bash_logout
-rw-r--r--   1 root     root     3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root     root      807 Feb 13  2026 .profile
-rw-r-----   1 bandit11 bandit10   69 Jun 24 14:58 data.txt
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIHBZZk9ZNkh3VXNEajVyTDlVdnloVTdNQ212OHZONVJvCg==
```

The password is base64 encoded so I decided to check out the command `base64`

![image](https://hackmd.io/_uploads/H1PR1i68zg.png)

Using the command:

```
bandit10@bandit:~$ base64 --decode data.txt
The password is pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

#### Password
```
pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```