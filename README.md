shadowsocks
===========

[![Build Status](https://travis-ci.org/clowwindy/shadowsocks.png)](https://travis-ci.org/clowwindy/shadowsocks)
Current version: 1.2.3

shadowsocks is a lightweight tunnel proxy which can help you get through firewalls

Other ports and clients can be found [here](https://github.com/clowwindy/shadowsocks/wiki/Ports-and-Clients).

Usage
-----------

First, make sure you have Python 2.6 or 2.7.

    $ python --version
    Python 2.6.8


Then edit `config.json`, change the following values:

    server          your server ip or hostname
    server_port     server port
    local_port      local port
    password        a password used to encrypt transfer
    method          encryption method, "bf-cfb", "aes-256-cfb", "des-cfb", "rc4", etc. Default is table


Put all the files on your server. Run `python server.py` on your server. To run it in the background, run `nohup python server.py > log &`.

Put all the files on your client machine. Run `python local.py` on your client machine.

Change the proxy setting in your browser into

    protocol: socks5
    hostname: 127.0.0.1
    port:     your local_port

Encryption
------------

If you want to use non-default encryption method like "bf-cfb", please install [M2Crypto](http://chandlerproject.org/Projects/MeTooCrypto).

Ubuntu:

    sudo apt-get install python-m2crypto

Others:

    pip install M2Crypto


Command line args
-----------------

You can use args to override settings from `config.json`.

    python local.py -s server_name -p server_port -l local_port -k password -m bf-cfb -b bind_address -6
    python server.py -p server_port -k password -m bf-cfb -6

Performance
------------

You may want to install gevent for better performance.

    $ sudo apt-get install python-gevent

Or:

    $ sudo apt-get install libevent-dev python-pip
    $ sudo pip install gevent

Troubleshooting
---------------

* I can only load some websites  
   Check the logs of local.py. If you see only IPs, not hostnames, your may got DNS poisoned, but your browser hasn't 
    been configured to let the proxy resolve DNS.  
   To set proper DNS config, you can simply install FoxyProxy / Autoproxy for Firefox, or ProxySwitchy / SwitchySharp for 
   Chrome. They will set the config in your browser automatically.  
   Or you can change network.proxy.socks_remote_dns into true in about:config page if you use Firefox.
* I can't load any websites and the log prints mode != 1  
    Make sure proxy protocol is set to Socks5, not Socks4 or HTTP.
* I use IE and I can't get my proxy to work    
    Since you can't specify Socks4 or Socks5 in IE settings, you may want to use a PAC(Proxy auto-config) script, or 
    just use Firefox instead.

License
-------
MIT

Bugs and Issues
----------------
Please visit [issue tracker](https://github.com/clowwindy/shadowsocks/issues?state=open)
