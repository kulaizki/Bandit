# Bandit 8

In this level, the password is a line of text that occurs `only once` in the file `data.txt`. 
With that, we can use the `sort` command to gather all duplicates and use the `uniq -u` command
to filter out duplicates for each line.

```bash
bandit8@bandit:~$ sort data.txt | uniq -u
EN632PlfYiZbn3PhVK3XOGSlNInNE00t
```

Note: uniq -u cannot be used alone since the lines must be sorted first.
