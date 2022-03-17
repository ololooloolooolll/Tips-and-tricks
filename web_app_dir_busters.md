# Web Site Directories

Web servers often have directories that may not be obvious.

Find out extra directories with these tools.

## Feroxbuster

```
feroxbuster --url http://my.target.com
```

Gobuster is threaded. Dirb is not.
Conversely...
Dirb can search recursively. Gobuster cannot.
Take that for what you will and your needs.

## Gobuster

General scan:

```
gobuster dir -u 10.10.10.1 -w /usr/share/wordlists/dirb/common.txt
```
**you have to run gobuster against all found directories**
10.10.10.1/uploads 10.10.10.1/images etc...

Specific file extension scan:

```
gobuster dir -u 10.10.10.1 -x .php -w /usr/share/wordlists/dirb/common.txt
```

## dirb

```
dirb http://my.target.com/
dirb http://my.target.com/ -X .html
dirb http://my.target.com/ /usr/share/dirb/wordlists/vulns/apache.txt
dirb dirbs http://my.securetarget.com/
```
