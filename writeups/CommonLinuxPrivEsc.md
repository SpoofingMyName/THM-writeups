# Common Linux Privilege Escalation

**INCOMPLETE - will update this eventually**

```

moving from non-privileged user to non-priviled user = horizontal escalation

moving from non-privileged user to privileged user = vetical escalation

```

## Exploiting Crontab

```

Cron = process that executes tasks at specific dates and times

e.g a task scheduler

if a task due to run is owned by root, but has weak perms, we can manipulate this

```

## Exploiting PATH 

```

Variable that stores locations of executable programs

can manipulate the variable to run a program of your choosing

script in user5's home directory that executes 'ls'

we can imitate this by creating our own executable named 'ls' in /tmp and modifying the $PATH variable to execute our ls executable rather than the system one

```
