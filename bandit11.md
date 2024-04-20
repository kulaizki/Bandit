In this level, we're given a file where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.
This is more commonly known as the **Caesar Cipher**. 

To solve this, we have to use the `tr` command to translate
the characters into our new pattern with the syntax `tr <old_chars> <new_chars>`.
```bash
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf WIAOOSFzMjXXBC0KoSKBbJ8puQm5lIEi
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
```
