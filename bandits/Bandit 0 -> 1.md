# Task
#### Log into the game using SSH
Server: bandit.labs.overthewire.org\
Port: 2220\
Username: bandit0\
Password: bandit0
# Solution
Reading the man page for ssh command we can log into bandit01 using the following command and flag:

```
ssh <username>@<host> -p <port>
```

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2200
bandit0
```

Read the **readme** file by using the following command:

```bash
cat readme
``` 

which gives the ouput 
```
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

#### Password: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
