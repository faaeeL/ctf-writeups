# Task
#### Read the file named `--spaces in this filename--` located in the home directory
Server: bandit.labs.overthewire.org
Port: 2220
Username: bandit2
Password: PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
# Solution

Using the command `cat --spaces in this filename--` would return the following

```bash
error: unexpected argument '--spaces' found

  tip: to pass '--spaces' as a value, use '-- --spaces'

Usage: cat [OPTION]... [FILE]...

For more information, try '--help'.
```

Instead we should include the character `\` to treat spaces as a part of the filename

```
bandit2@bandit:~$ cat ./--spaces\ in\ this\ filename--
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

#### Password: 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME