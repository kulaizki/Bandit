we use `/` to specify the root dir, `-type f` to specify that it is a regular file type, `-user` and `-group` 
to specify the user and group of the file, then `2>/dev/null` to discard error outputs such as having no
permission to open the scanned file and find the file we are looking for alone
```bash
bandit6@bandit:~$ ls
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
cat /var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
```
