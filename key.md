# Key Notes
- `ls -la, cd, cat, touch `
- `less`
- `file `
- `file ./*`
- `grep`
- `uniq -u`
- `find /path -name filename 2>/dev/null`
- `tr 'A-Za-z' 'N-ZA-Mn-za-m'`
- `base64 -d`
- `strings filename`
- `sort filename | uniq -u`
- `mv oldname newname` (*useful for converting to gz/bz2 to decompress*)
- `xxd -r` (*hex dump*)
- `gzip -d`
- `bzip2 -d`
- `cat hexdump_data | head`
- `ssh-agent`
- `nc ip port`
- `ssh-add privatekey`
- `ssh -i sshkey.private user@remote -p port`
- `cat filename | nc remote_server_ip port`
- `echo filename | nc remote_server_ip port`
- `ssh -i privatekey username@remote port`
- `openssl s_client localhost:30001` (*for TLS or SSH encryption*)
- `eval "$(ssh-agent -s)" `
- `chmod` 
	- `u+r, go-w, a+x, 644, 755 dir,`
	- `-r 600 dir, 777, +s, +t dir`
	- `[chmod -rwx file]`
	- `[chmod u+r,g+w,o-x file]`
- `nmap -sV host -p port/s`
	- `openssl s_client -connect localhost:30001`
- `diff file file`
- `ssh user@remote -p 2220 cat readme` (for auto log-out .bashrc)
- `ls -l / file, ls -la, ls -ls`
- `./bandit20-do cat` {**setuid binary**} (*run a command with the privileges of another user*)
	- `./bandit20-do cat /etc/bandit_pass/bandit20`
- `nc -l -p port` (listening / creates a server)
	- `echo "pass" | nc -l -p port`
- `cron, crontab, cronjob` (daemon to execute scheduled jobs / commands)
- `cp file file` 
- `grev -v` (exclude)

```sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo || exit 1
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -rf ./$i
    fi
done
```
`chmod 777` (for all access bandit 24 to bandit 23)

## Bandit 17 RSA KEY
```bash
-----BEGIN RSA PRIVATE KEY----- MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama +TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT 8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM 77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3 vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY= 
-----END RSA PRIVATE KEY-----
```

## Passwords
```bash
1: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
2: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx
3: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
4: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
5: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
6: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
7: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
8: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
9: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
10: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
11: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
12: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
13: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
14: MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
15: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
16: kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
17: EReVavePLFHtFlFsjn3hyzMlvSuSAcRD
18: x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
19: cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
20: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
21: EeoULMCra2q0dSkYj561DX7s1CpBuOBt
22: tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
23: 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
24: gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```
