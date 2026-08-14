# Task 
#### The password for the next level is stored **somewhere on the server** and has all of the following properties:
- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

Server: bandit.labs.overthewire.org\
Port: 2220\
Username: bandit6\
Password: pXa26xhMWaC2SvDotA4r9EgZkulOeSBW

# Solution

Using hints from the task:

```
bandit6@bandit:~$ cd /
bandit6@bandit:/$ find -type f -user bandit7 -group bandit6 -size 33c
find: ‘./snap’: Permission denied
find: ‘./lost+found’: Permission denied
find: ‘./manpage/manpage3-pw’: Permission denied
find: ‘./drifter/drifter14_src/axTLS’: Permission denied
find: ‘./run/pam_pidns’: Permission denied
find: ‘./run/udisks2’: Permission denied
find: ‘./run/chrony’: Permission denied
find: ‘./run/user/11025’: Permission denied
...
```

There are a lot of `Permission denied` messages since we don't have permission for those files, we can append the tag `2>dev/null` to hide all the error messages.

```
bandit6@bandit:/$ find -type f -user bandit7 -group bandit6 -size 33c 2>dev/null
./var/lib/dpkg/info/bandit7.password
```

Reading the file:

```
bandit6@bandit:/$ cat ./var/lib/dpkg/info/bandit7.password
Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
```

#### Password
```
Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
```

