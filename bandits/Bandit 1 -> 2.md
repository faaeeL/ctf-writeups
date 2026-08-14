# Task
#### Read the file named - located in the home directory
Server: bandit.labs.overthewire.org\
Port: 2220\
Username: bandit1\
Password: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
# Solution
Using the command `cat -` would not return anything as `-` is a standard option character for Unix. (We can see that it's used for flags)

So instead we can include the path and use the command:
```bash
cat ./-
```

#### Password: 
```
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```