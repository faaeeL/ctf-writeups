---
title: Task

---

# Task
> The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

Server: bandit.labs.overthewire.org
Port: 2220
Username: bandit12
Password: GROozWPO8QyN0mGrjUkID0WCYkZiQxrN

# Solution

```
bandit12@bandit:~$ ls -la
total 24
drwxr-xr-x   2 root     root     4096 Jun 24 14:58 .
drwxr-xr-x 150 root     root     4096 Jun 24 15:02 ..
-rw-r--r--   1 root     root      220 Feb 13  2026 .bash_logout
-rw-r--r--   1 root     root     3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root     root      807 Feb 13  2026 .profile
-rw-r-----   1 bandit13 bandit12 2639 Jun 24 14:58 data.txt
```

Doing what the task suggest:

```
bandit12@bandit:~$ mktemp -d
/tmp/tmp.awOZ3qGkpF
bandit12@bandit:~$ cp data.txt 
bandit12@bandit:~$ cp data.txt /tmp/tmp.awOZ3qGkpF
bandit12@bandit:~$ cd /tmp/tmp.awOZ3qGkpF
```

Trying to read the file:

```
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ ls    
data.txt
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ cat data.txt
00000000: 1f8b 0808 b2f0 3b6a 0203 6461 7461 322e  ......;j..data2.
00000010: 6269 6e00 0142 02bd fd42 5a68 3931 4159  bin..B...BZh91AY
00000020: 2653 59dc 0966 8300 001a ffff dff5 c5fe  &SY..f..........
...
```

Checking out the `xxd` command:

![image](https://hackmd.io/_uploads/HyNwmj6Ufg.png)

```
  - Revert a plaintext hexdump back into binary, and save it as a binary file:
    xxd -revert -postscript input_file output_file
```

When I used the command and check what file type it became:

```
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ xxd -revert -postscript data.txt file1
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ file file1                            
file1: data
```

However if I don't use the flag `-postscript` it became:

```
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ xxd -revert data.txt file1            
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ file file1                
file1: gzip compressed data, was "data2.bin", last modified: Wed Jun 24 14:58:58 2026, max compression, from Unix, original size modulo 2^32 608
```

Using the `gzip` command to decompress:

```
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ gzip --decompress file1   
gzip: file1: unknown suffix -- ignored
```

Since gzip doesn't decompress the file due to not having a suitable suffix, I renamed the file to `file1.gz` instead, and with some more decompressing later:

```
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ mv file1 file1.gz
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ gzip --decompress file1.gz

gzip: file1.gz: decompression OK, trailing garbage ignored
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ ls
data.txt  file1
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ file file1
file1: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ bzip2 --decompress file1
bzip2: Can't guess original name for file1 -- using file1.out
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ ls
data.txt  file1.out
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ file file1.out
file1.out: gzip compressed data, was "data4.bin", last modified: Wed Jun 24 14:58:58 2026, max compression, from Unix, original size modulo 2^32 20480
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ mv file1.out file1.gz
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ gzip --decompress file1.gz
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ ls                        
data.txt  file1
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ file file1
file1: POSIX tar archive (GNU)
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ tar -xf file1
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ ls
data.txt  data5.bin  file1
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ file data5.bin
data5.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ tar -xf data5.bin
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ ls               
data.txt  data5.bin  data6.bin  file1
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ bzip2 --decompress data6.bin
bzip2: Can't guess original name for data6.bin -- using data6.bin.out
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ file data6.bin.out
data6.bin.out: POSIX tar archive (GNU)
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ tar -xf data6.bin.out
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ ls
data.txt  data5.bin  data6.bin.out  data8.bin  file1
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Wed Jun 24 14:58:58 2026, max compression, from Unix, original size modulo 2^32 49
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ mv data8.bin file2.gz
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ gzip --decompress file2.gz
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ ls
data.txt  data5.bin  data6.bin.out  file1  file2
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ file file2
file2: ASCII text
bandit12@bandit:/tmp/tmp.awOZ3qGkpF$ cat file2
The password is qQYQiHOBPR8zR61qxYqX45quvihF2uzk
```

#### Password

```
qQYQiHOBPR8zR61qxYqX45quvihF2uzk
```