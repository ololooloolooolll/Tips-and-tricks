# Password cracking

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

