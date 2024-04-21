# Key Notes
- `ls -la, cd, cat, touch `
- `less`
- `file `
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
- `ssh-agent`
- `nc ip port`
- `ssh-add privatekey`
- `ssh -i sshkey.private user@remote -p port`
- `cat filename | nc remote_server_ip port`
- `echo filename | nc remote_server_ip port`
- `ssh -i privatekey username@remote port`
- `openssl s_client -connect localhost:30001` (*for TLS or SSH encryption*)
- `eval "$(ssh-agent -s)" `
- `chmod `
	- `u+r, go-w, a+x, 644, 755 dir`, 
	- `-r 600 dir, 777, +s, +t dir` 
	- `[chmod -rwx file]`
	- `[chmod u+r,g+w,o-x file]`
- `nmap -sV host -p port/s`
- `diff file file`
- `ssh user@remote -p 2220 cat readme` (for auto log-out .bashrc)
- `ls -l / file, ls -la, ls -ls`
- `./bandit20-do cat` {**setuid binary**} (*run a command with the privileges of another user*)
- `nc -l -p port` (listening / creates a server)
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
