In this level, we need to find the password in the file `data.txt` next to the word `millionth`. 
Since there are too many words in data.txt, we have to use the command `grep` to find
the pattern/word we want and filter that from everything else.
```bash
bandit7@bandit:~$ grep millionth data.txt
millionth	TESKZC0XvTetK0S9xNwm25STk5iWrBvP
```
