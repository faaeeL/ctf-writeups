---
title: Task

---

# Task
> The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Look at the commands that logged you into previous bandit levels, and find out how to use the key for this level.
If you need help with this level: a hint file can be found in the home directory.
Make sure to read the error messages as they are informative.

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit13\
Password: qQYQiHOBPR8zR61qxYqX45quvihF2uzk

# Solution

Checking the files and reading the hint provided:

```
bandit13@bandit:~$ ls -la
total 28
drwxr-xr-x   2 root     root     4096 Jun 24 14:59 .
drwxr-xr-x 150 root     root     4096 Jun 24 15:02 ..
-rw-r--r--   1 root     root      220 Feb 13  2026 .bash_logout
-rw-r--r--   1 root     root     3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root     root      807 Feb 13  2026 .profile
-rw-r-----   1 bandit14 bandit13  467 Jun 24 14:59 HINT
-rw-r-----   1 bandit14 bandit13 2602 Jun 24 14:59 sshkey.private
bandit13@bandit:~$ cat HINT
If you have trouble with this level, note the following:

1) As for all other levels, this level has a website with information:
   https://overthewire.org/wargames/bandit/bandit14.html
2) No, the level is not broken. To verify, see:
   https://status.overthewire.org/
3) The current version of OverTheWire prevents logging in from one
   level to another via localhost. Log out, and see 1)
4) If you get errors, read the error message on your screen.
   We mean it!
```

Trying to login into bandít14 using the ssh key provided:

```
bandit13@bandit:~$ ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220                                         
The authenticity of host '[bandit.labs.overthewire.org]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is: SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit13/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit13/.ssh/known_hosts).
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

!!! You are trying to log into this SSH server with a password on port 2220 from localhost.
!!! Connecting from localhost is blocked to conserve resources.
!!! Please log out and log in again.
```

Checking out what the command `scp` do:

<img width="921" height="740" alt="image" src="https://github.com/user-attachments/assets/cf04011d-e179-400f-b91b-7e4b7bc2aee0" />


I can see the that command `scp` allows me to copy a file from a remote host to my local directory.

Since we can't login into bandit14 while being user bandit13, we instead can copy the `sshkey.private` file to our local directory and login directly.

<img width="904" height="387" alt="image" src="https://github.com/user-attachments/assets/dc83f64a-971f-44e6-82ee-660b90cf9f2f" />


I can see that the `sshkey.private` file is in my computer:

<img width="862" height="94" alt="image" src="https://github.com/user-attachments/assets/beec5e15-824e-46e2-9978-531a16e7dcb4" />

Login into user bandit14:

<img width="905" height="484" alt="image" src="https://github.com/user-attachments/assets/b9a79df0-a1fe-44a6-8d5b-ae1247b2572e" />

I couldn't login due to the key file being too open.

So we can change the permission using the command `chmod 700 sshkey.private`

with:
- 7 being the user can read, write, and execute.
- 0 being the group can't do either of those.
- the second 0 being others can't do either of those.

Trying to login again:

<img width="885" height="714" alt="image" src="https://github.com/user-attachments/assets/5b466409-86f5-4402-ad70-4a756b547fce" />

Since the password is in `/etc/bandit_pass/bandit14` we can read the file now and find out what the password is:

```
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

#### Password
```
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```
