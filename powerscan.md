# MASSCAN and NMAP

Two very powerfull tools to scan hosts are masscan and nmap. 

There is alot to know to unleash the true power of these tools, these general commands will help in most cases.

This scanning technique only works for single hosts, very good in CTF like challenges.

## Masscan super scan

First, run a mass scan to all tcp and udp ports, redirect output to a file: 

    masscan -p1-65535,U:1-65535 target.local --rate=100000 -e eth0 --wait 5 > mascan-target.txt
    
Second, run an Nmap against the output of masscan:

    /home/user/scripts/parse_mscan.py; while read each; do sudo nmap -sV -O -sC -sS -sU $each; done < nmap.txt
    
