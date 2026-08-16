---
title: Bandit 22 -> 23

---

# Task
>A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

>NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit22\
Password: RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz

# Solution

Navigating and checking files:
```
bandit22@bandit:~$ cd /etc/cron.d/                                              
bandit22@bandit:/etc/cron.d$ ls -la
total 56
drwxr-xr-x   2 root root  4096 Jul  3 16:19 .
drwxr-xr-x 124 root root 12288 Jun 25 12:37 ..
-rw-r--r--   1 root root   102 Nov  5  2025 .placeholder
-r--r-----   1 root root    47 Jun 24 14:59 behemoth4_cleanup
-rw-r--r--   1 root root   127 Jul  3 16:19 clean_tmp
-rw-r--r--   1 root root   120 Jun 24 14:59 cronjob_bandit22
-rw-r--r--   1 root root   122 Jun 24 14:59 cronjob_bandit23
-rw-r--r--   1 root root   120 Jun 24 14:59 cronjob_bandit24
-rw-r--r--   1 root root   188 Feb 13  2026 e2scrub_all
-r--r-----   1 root root    48 Jun 24 15:01 leviathan5_cleanup
-rw-------   1 root root   138 Jun 24 15:01 manpage3_resetpw_job
-rwx------   1 root root    52 Jun 24 15:03 otw-tmp-dir
bandit22@bandit:/etc/cron.d$ file *
behemoth4_cleanup:    regular file, no read permission
clean_tmp:            ASCII text
cronjob_bandit22:     ASCII text
cronjob_bandit23:     ASCII text
cronjob_bandit24:     ASCII text
e2scrub_all:          ASCII text
leviathan5_cleanup:   regular file, no read permission
manpage3_resetpw_job: regular file, no read permission
otw-tmp-dir:          regular file, no read permission
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```

Reading the bash script:

```
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh 
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

So the script assign the `myname` variable using the command `whoami`, in this case it would be `bandit23` since it is ran under user bandit23.

Then it assigns the `mytarget` variable with some voodoo magic (I have no idea what `md5sum` does but I do know that `cut -d ' ' -f 1 ` means using space as a delimiter and only prints out the first field)

Then it copy the password from `myname` file to `mytarget` file

So we can use the same command but replace `$myname` with `bandit23`

```
bandit22@bandit:/etc/cron.d$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@bandit:/etc/cron.d$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw
```


# Password
```
gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw
```