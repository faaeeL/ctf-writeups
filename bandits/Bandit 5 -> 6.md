# Task
#### The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:
- human-readable
- 1033 bytes in size
- not executable

Server: bandit.labs.overthewire.org\
Port: 2220\
Username: bandit5\
Password: 6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
# Solution
Navigating through files:

```
bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere04  maybehere08  maybehere12  maybehere16
maybehere01  maybehere05  maybehere09  maybehere13  maybehere17
maybehere02  maybehere06  maybehere10  maybehere14  maybehere18
maybehere03  maybehere07  maybehere11  maybehere15  maybehere19
```

We can see a lot of directories in **inhere**

Checking what's in the first folder:

```
bandit5@bandit:~/inhere$ cd maybehere00
bandit5@bandit:~/inhere/maybehere00$ ls
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3
bandit5@bandit:~/inhere/maybehere00$ 
```

Checking another folder

```
bandit5@bandit:~/inhere/maybehere00$ cd ..
bandit5@bandit:~/inhere$ cd maybehere01
bandit5@bandit:~/inhere/maybehere01$ ls
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3
bandit5@bandit:~/inhere/maybehere01$ 
```

I can assume that all the folders would contain the samething, checking them one by one would take a long time

Using the hint provided by the website, checking out the `find` command using `tldr`:

![[tldr_find.png]]

with more information from [man page](https://manned.org/find)

Using the command `find -type f -size 1033c ! -executable`

```
bandit5@bandit:~/inhere$ find -type f -size 1033c ! -executable
./maybehere07/.file2
```

with
- `-type f` to find a file type
- `-size 1033c` according to the level (using `c` for bytes)
- `! -executable` to find files that are not executable

Checking if it's human readable:

```
bandit5@bandit:~/inhere$ file ./maybehere07/.file2
./maybehere07/.file2: ASCII text, with very long lines (1000)
```

Reading the file:

```
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```

#### Password

```
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```
