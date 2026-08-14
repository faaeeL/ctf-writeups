# Task
#### Read a hidden file in the **inhere** directory
Server: bandit.labs.overthewire.org
Port: 2220
Username: bandit3
Password: 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
# Solution
Navigate to the inhere directory using the command:

```bash
cd inhere
```

Using the command `ls` would not return anything as the file we're looking for is hidden.
Instead we can use the flag `-a` to not ignore entries with `.` and `..` (hidden files)

```
bandit3@bandit:~/inhere$ ls -a
.  ..  ...Hiding-From-You
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

#### Password: xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq

