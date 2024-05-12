# Bandit 14

We can retrieve the password for the next level by submitting the password of the current level to `port 30000` on `localhost`
using `netcat` **(nc)**.

```bash
bandit14@bandit:~$ nc localhost 30000
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
Correct!
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
```
