---
title: Bandit 20 -> 21

---

# Task
>There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

>NOTE: Try connecting to your own network daemon to see if it works as you think

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit20\
Password: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA

# Solution

Navigating and checking:

```
bandit20@bandit:~$ ls                                                                    suconnect                                                   
bandit20@bandit:~$ file suconnect
suconnect: setuid ELF 32-bit LSB executable, Intel i386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, BuildID[sha1]=f5f4e327efe53d15fcf0c0fb08324d5f939ac4f0, for GNU/Linux 3.2.0, not stripped
bandit20@bandit:~$ ./suconnect
Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.
```

![image](/pngs/bandit20_21.png)

Using `nc` (netcat) I can start listening on a specific port.

I tried doing `nc -l -p 1234`. However it would put me at a standstill since it's still listening until a connection is made.

In order to run the process in the background I have to include the tag `&`.

The setuid binary provided only connect to a given port and check if it receives the correct password.

In order to send a password to the other side I'd have to use the command `echo` to output the string, alongside with the pipe `|`.

```
bandit20@bandit:~$ echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA" | nc -l -p 1234 &
[1] 68
bandit20@bandit:~$ ./suconnect 1234                                         
Read: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
Password matches, sending next password
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
[1]+  Done                       echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA" | nc -l -p 1234
bandit20@bandit:~$ 
```

# Password
```
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
```