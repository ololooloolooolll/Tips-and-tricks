# Routing traffic from specific host to specific destination

1. make sure you route

2.  add DNAT rule

3.  Add masquerade rule

```
sysctl -w net.ipv4.ip_forward=1
iptables -t nat -A PREROUTING -s 192.168.100.1/32 tcp -j DNAT --to-destination 192.168.200.2
iptables -t nat -A POSTROUTING -s 192.168.100.1/32 tcp -j MASQUERADE
```
