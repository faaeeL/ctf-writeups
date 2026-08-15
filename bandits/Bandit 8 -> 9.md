---
title: Task

---

# Task
#### The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

Server: bandit.labs.overthewire.org
Port: 2220
Username: bandit8
Password: 

# Solution

Navigating through files:

```
bandit8@bandit:~$ ls -la
total 56
drwxr-xr-x   2 root    root     4096 Jun 24 14:59 .
drwxr-xr-x 150 root    root     4096 Jun 24 15:02 ..
-rw-r--r--   1 root    root      220 Feb 13  2026 .bash_logout
-rw-r--r--   1 root    root     3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root    root      807 Feb 13  2026 .profile
-rw-r-----   1 bandit9 bandit8 33033 Jun 24 14:59 data.txt
```

Reading the file:

```
bandit8@bandit:~$ cat data.txt
tob2Ifz9ZpTlahbsHpV9rHyxKYV50E6d
b5l3vW4lfE58gjIRcgZmRgOQ3L7LL4rE
TbJy4tkWD7DM0ImHuy0AM5LdDee0kx7d
7GeeWiLeZOXFxt4V5fuEo3JjOJU73ByA
zlVs1t1ZAwNkYoJeu2keu1XDb379Enps
bTfG6I2cS7MdEYNinodFJJRxYmaAufgL
vtiBxlHKiVDnhAQx2KVW52LvbHlqOyMw
4a3V4yuHto5mAtM692NCfPenjZAOh0Mq
RR5uDrH1FfZrRlQJfwD2vuJYu3gkVLV8
tRzoA6qo8w2WjMhQI2BYblWD6A2EH9Rm
tob2Ifz9ZpTlahbsHpV9rHyxKYV50E6d
EHQRR7ZeLHpdAtGgpvjt1Lcfp9A2Tiz8
...
```

Using hints from the website I can assume that I'll be using `sort` or `uniq`

Viewing what `sort` command do:

![image](https://hackmd.io/_uploads/SkvB956IGe.png)


I can see:
```
  - Sort a file preserving only unique lines:
    sort --unique path/to/file
```

So I tried that command first:

```
bandit8@bandit:~$ sort --unique data.txt       
0waJL8EA3cLE0pXxTKPoRC2xcwUt0ET4
2cAz036IkVk6SrCESpZf0oo480Iu2MNg
2VQBoUDLANB83noigdG5tVFcARrooQsS
3cBxNlgpPIC3bEq6znuHJcHcY4POK5Dh
3l40QNwtoDvmEOVaE2LWoszZBbsB5A77
3mjCvj0RPgn8IrXX1eHJVAKRoJOAB1AA
4a3V4yuHto5mAtM692NCfPenjZAOh0Mq
...
```

Although the output is shorter, but there are still a lot of 'fake' passwords.

I see that I might have misunderstood what the command really do.

The command doesn't output the line with no replicas but it ignore lines which are copies of another line.

Viewing what `uniq` do:

![image](https://hackmd.io/_uploads/B1z-ncaUMl.png)

```
  - Display only unique lines:
    sort path/to/file | uniq --unique
```

Trying out the command:

```
bandit8@bandit:~$ sort data.txt | uniq --unique
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```

#### Password
```
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```