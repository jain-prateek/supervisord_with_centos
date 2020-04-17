# supervisord_with_centos
code to run a python script using supervisord and creating logs of script.

First install supervisord

yum install supervisor

service supervisord status : it should be inactive

Now go to directory /etc/supervisord.d/

Create a new .ini file script.ini and paste following content inside it:

[program:test_script]
command=python3 /home/test.py
autostart=true
autorestart=true
stderr_logfile=/var/log/test.err.log
stdout_logfile=/var/log/test.out.log


Now run service supervisord start

You can watch supervisor logs at : /var/log/supervisor/supervisord.log

And you can watch your script logs at : /var/log/test.err.log and /var/log/test.out.log

your test.py scripts shoul contain:
import time
import sys

def test():
    while True:
        print("hello testing", flush=True)
        time.sleep(30)

if __name__ == "__main__":
    test()
    
For pushing all logging from script to supervisord logs use:
import time
import sys
import logging

logging.basicConfig(stream=sys.stdout, level=logging.INFO)

def test():
    while True:
        logging.info("test222")
        logging.error("test4444")
        print("hello testing")
        print("")
        time.sleep(30)

if __name__ == "__main__":
    test()
    
ORR
use print statement like this : print("hello world", flush=True)

Thats it for today!!!!!!
