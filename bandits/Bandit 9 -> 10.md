# Task
#### The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

Server: bandit.labs.overthewire.org
Port: 2220
Username: bandit9
Password: EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl

# Solution

Checking out files:

```
bandit9@bandit:~$ ls -la 
total 40
drwxr-xr-x   2 root     root     4096 Jun 24 14:58 .
drwxr-xr-x 150 root     root     4096 Jun 24 15:02 ..
-rw-r--r--   1 root     root      220 Feb 13  2026 .bash_logout
-rw-r--r--   1 root     root     3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root     root      807 Feb 13  2026 .profile
-rw-r-----   1 bandit10 bandit9 19382 Jun 24 14:58 data.txt
```

Reading the file:

```
bandit9@bandit:~$ cat data.txt
�
�j"+V[��ot��je}<��99��6I%���Q���
7���^X�����plM&]��Gl�J��O��))Q�u
                                1y1J�h?H�Z��g�̾Ε�ݭ3�r�&}�7��4�=�#5�e
                                                                   +�9���u*-D@6@�17�G��(]7�D[�������"�+v�$��5�8t�����h�Fr�N����
                                                                   ...
```

Trying to see lines with the character `=` using `grep`

```
bandit9@bandit:~$ cat data.txt | grep =  
grep: (standard input): binary file matches
```

I can't grep the character `=` because there are character encoding in the files.

Checking out what the `strings` command do:

![image](https://hackmd.io/_uploads/S1mxkspLfx.png)

Using `strings` with `grep`:

```
bandit9@bandit:~$ strings data.txt | grep =
=KGEn
cL0========== the
=<P& 
========== password
bU=\
a7=P
>========== is
wbp=
=lR(
a=-io
R========== B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
)=Lc
x=E$
```

#### Password
```
B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```