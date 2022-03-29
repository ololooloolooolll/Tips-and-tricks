# SSH Tunneling

How to tunnel your traffic using SSH to traverse DMZ and reach private networks.

## Local Port Forwarding 

This type of SSH forwarding will transfer a connection from the desired client host to the destined SSH server host and then move the traffic to the destination host port.

Forward traffic to a local database server from a public server:

```
# ssh -L [LOCAL_IP:]LOCAL_PORT:DESTINATION:DESTINATION_PORT [USER@]SSH_SERVER
# ssh -L 1.1.1.1:3306:db02.host.net:3306 user@public.host.net
```

## Remote Port Forwarding 

This type of SSH forwarding is the complete opposite of the local port forwarding method. The remote forwarding will allow the user to forward a port available on the remote server machine to the port available on the local machine.

```
# ssh -R [REMOTE:]REMOTE_PORT:DESTINATION:DESTINATION_PORT [USER@]SSH_SERVER
# ssh -R 192.168.10.1:8010:127.0.0.1:3100 -N -f user_name@remote.host.net
```

## Dynamic Port Forwarding

Probably the most powerful

With the help of dynamic port forwarding, you can create a socket on the local machine that will act as a SOCKS proxy server.

1. On the pwned1 server, create a socks proxy:

```
user@pwned1$ ssh -D 127.0.0.1:9052 user@localhost
```

2. On redir1, create a remote port forwarding tunnel:

```
weak@redir1$ ssh -R 127.0.0.1:9051:127.0.0.1:9052 weak@localhost
```

3. From the internet, scan the private network:

```
root@bt# sed -i '^socks4/s/socks4/socks5' /etc/proxychains4.conf
root@bt# sed -i '^socks5/s/9050/9051' /etc/proxychains4.conf
root@bt# proxychains nmap -sT -p 445 192.168.1.10
```


## Use case

General example were you need to cross mutiple secuirty zones:

| Host | Outside | Inside |
| Evil | 1.1.1.1 | 192.168.1.18 |
| PubSrv | 192.168.1.22 | 172.16.4.22 |
| PriSrv | 172.16.4.30 | 10.10.10.30 |
| DC01   | 10.10.10.10 | 127.0.0.1 |


1. From the Evil host, connect to the PubSrv

```
evil@bt# ssh -f -N -D 9050 user@192.168.1.22
   <password>
```

2. Setup a second tunnel within the first

**The default /etc/proxychains4.conf uses 9050**

This command connects to PubSrv:9050 and runs another tunnel on port 10050:

```
evil@bt# proxychains ssh -f -N -D 10050 internal_user@172.168.4.30 -p 2222
```

3. Reach the domain controller from the pub_srv

**Edit the proxychains4.conf file to use 10050 instead of 9050**

Now, by using the proxychains on port 10050, you should be able to reach the domain controller and scan the network

```
evil@bt# proxychains nmap -sT 10.0.10.10 -p 445
evil@bt# proxychains rdesktop 10.10.10.10 -u Administrator -p password -g 90%
```
