# Task 
#### The password for the next level is stored in the file **data.txt** next to the word **millionth**
Server: bandit.labs.overthewire.org\
Port: 2220\
Username: bandit7\
Password: Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
# Solution

Navigating:

```
bandit7@bandit:~$ ls -la
total 4108
drwxr-xr-x   2 root    root       4096 Jun 24 14:59 .
drwxr-xr-x 150 root    root       4096 Jun 24 15:02 ..
-rw-r--r--   1 root    root        220 Feb 13 12:16 .bash_logout
-rw-r--r--   1 root    root       3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root    root        807 Feb 13 12:16 .profile
-rw-r-----   1 bandit8 bandit7 4184396 Jun 24 14:59 data.txt
```

Seeing the size of the `data.txt` we can deduct that it contain a lot of text.

Checking the file using `cat` returns a lot of text lines.

Checking the command `grep` using `tldr`

![find](/pngs/tldr_find.png)

Reading the text file with `grep`:

```
bandit7@bandit:~$ cat data.txt | grep millionth
millionth	VR1ljMayciFxbnUokuQmJFw6QC9VKtub
```

#### Password
```
VR1ljMayciFxbnUokuQmJFw6QC9VKtub
```
