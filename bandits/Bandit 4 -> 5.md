# Task
#### Find the only human-readable file in the **inhere** directory 
Server: bandit.labs.overthewire.org\
Port: 2220\
Username: bandit4\
Password: xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
# Solution

Listing and navigate through the files:

```
bandit4@bandit:~$ ls                                                                   
inhere
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```

Reading one of the files:

```
bandit4@bandit:~/inhere$ cat ./-file00
Y1[�b1���� ��ɂ�D¬1K0
                    3'���bandit4@bandit:~/inhere$ 
```

Reading through all the files one by one would be a hassle, since the file we need is human-readable we can check the file type of all the files present in the folder using the command `file ./* `:

```
bandit4@bandit:~/inhere$ file ./* 
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: OpenPGP Public Key
./-file07: ASCII text
./-file08: data
./-file09: Motorola S-Record; binary data in text format
```

We can see that `-file07` is in ASCII text.

Reading file `-file07`
```
bandit4@bandit:~/inhere$ cat ./-file07
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```

#### Password: 
```
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```