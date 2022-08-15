# Password cracking

## Common passwords

1. save the sample hash to a file

```
$6^zS7kHfFMg3aYht4$1IUrhZanRuDZhf1oIdnoOvXoolKmlwbkegBXk.VtGg78eL7WBM60rNtGbZxKBtPu8Ufm9hM0R/BLdACoQ0T9n/
```

2. Use this command to crack the password

```
~/# hashcat ~/hashes/crackme.hash /opt/wordlist/rockyou.txt
```

3. Read the cracked password

```
~/# hashcat --show
1800 | sha512crypt $6$, SHA512 (Unix) | Operating System
$6^zS7kHfFMg3aYht4$1IUrhZanRuDZhf1oIdnoOvXoolKmlwbkegBXk.VtGg78eL7WBM60rNtGbZxKBtPu8Ufm9hM0R/BLdACoQ0T9n/:ilovehacking
```

---

## Partially known passwords

1. get the hash you're looking for.

In this example, here is a common topology for passwords: Company Name + Year + special char + special char.

```
echo -ne 'Ecorp2022!!' | md5sum
a19a23367dfd388f52c6a55205586646  -
```

2. build the hashcat command
 
When you know someone uses that topology you can take advantage and crack an 11 char password in no time

```
hashcat -a3 -m0 a19a23367dfd388f52c6a55205586646 -1?u?l -2?l?d?s -3?s -4?d ?1corp202?4?3?3
```

Command explained:
$0 : hashcat, tool invoke
$1 : -a3, mode masked
$2 : -m0, md5 hash
$3 : a19a23367dfd388f52c6a55205586646, value of hash
$4 : -1?u?l, the ?1 character is either uppercase or lowercase
$5 : -2?l?d?s, the ?2 character is either a lowercase, digit or special character 
$6 : -3?s, the ?3 character must be special characters
$7 : -4?d, the ?4 is a digit
$8 : ?1c?2rp202?4?3?3, the password looks like this

topology hints:
- May or may not start with a captial letter
- "Ecorp" might have been spelt with a '0' in 1337speak
- Year might have been 2020, 2021 or 2022..
- Ends with two special characters

** ?1c?2rp202?4?3?3 = Upper_or_Lower_e , c , 0_o_or_O , r , p , Year(202) , 0_1_2 , Special_char , Special_char**

```
Host memory required for this attack: 0 MB

a19a23367dfd388f52c6a55205586646:Ecorp2022!!

Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 0 (MD5)
Hash.Target......: a19a23367dfd388f52c6a55205586646

-------
$ hashcat -a3 -m0 a19a23367dfd388f52c6a55205586646 --show                            
a19a23367dfd388f52c6a55205586646:Ecorp2022!!
```

