In this level, we use `strings` to filter the printable strings in `data.txt` as the file contains
lots of unreadable data. Then we use `grep` to find lines that contain multiple `=`.
```bash
bandit9@bandit:~$ strings data.txt | grep ===
x]T========== theG)"
========== passwordk^
========== is
========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
```
