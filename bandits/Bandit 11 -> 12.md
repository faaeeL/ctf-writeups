---
title: Task

---

# Bandit 11 -> 12
# Task
#### The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

Server: bandit.labs.overthewire.org
Port: 2220
Username: bandit11
Password: pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro

# Solution

```
bandit11@bandit:~$ ls -la
total 24
drwxr-xr-x   2 root     root     4096 Jun 24 14:58 .
drwxr-xr-x 150 root     root     4096 Jun 24 15:02 ..
-rw-r--r--   1 root     root      220 Feb 13  2026 .bash_logout
-rw-r--r--   1 root     root     3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root     root      807 Feb 13  2026 .profile
-rw-r-----   1 bandit12 bandit11   49 Jun 24 14:58 data.txt
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf TEBbmJCB8DlA0zTewHxVQ0JPLxMvDkeA
```

Reading the wikipedia page provided by the website ((ROT13)[https://en.wikipedia.org/wiki/ROT13]).

I can see the command:

```
$ # Map upper case A-Z to N-ZA-M and lower case a-z to n-za-m
$ tr 'A-Za-z' 'N-ZA-Mn-za-m' <<< "Pack My Box With Five Dozen Liquor Jugs"
Cnpx Zl Obk Jvgu Svir Qbmra Yvdhbe Whtf
```

So I could just reverse the command:

```
bandit11@bandit:~$ tr 'N-ZA-Mn-za-m' 'A-Za-z' <<< "Gur cnffjbeq vf TEBbmJCB8DlA0zTewHxVQ0JPLxMvDkeA"
The password is GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```

#### Password
```
GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```
