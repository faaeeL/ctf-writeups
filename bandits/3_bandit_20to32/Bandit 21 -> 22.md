---
title: Bandit 21 -> 22

---

# Task
>A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit21\
Password: bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY

# Solution

Navigating and checking files:
```
bandit21@bandit:~$ cd /etc/cron.d/
bandit21@bandit:/etc/cron.d$ ls
behemoth4_cleanup  cronjob_bandit23  leviathan5_cleanup
clean_tmp          cronjob_bandit24  manpage3_resetpw_job
cronjob_bandit22   e2scrub_all       otw-tmp-dir
bandit21@bandit:/etc/cron.d$ ls -la
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
```

Reading the cronjob for bandit22:

```
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

I can see that it runs the file `cronjob_bandit22.sh` as user bandit22 every minute (indicate by the 5 stars *)

So I try to read what the bash file does:

```
bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```
We can see that it changes the permission of the file `t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`

with
- 6 being owner have read and write permissions
- 4 being groups have read permission
- the last 4 means others have read permission

Then it reads the file `bandit22` and `>` means it copy the input into the `t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv` file

So we can read the `t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv` file for the password

```
bandit21@bandit:~$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz
```

# Password
```
RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz
```