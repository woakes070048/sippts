Sipscan is a very fast scanner for SIP services over UDP. It uses multithread and can scan large ranges of networks.

# Features #
Sipscan works sending and waiting well formed SIP packages. For example, Nmap is a great tool for network's scanning, but over UDP is better and quicker sending well formed packages and waiting for valid responses.

Sipscan by default try to connect over UDP protocol. If the connection fails then will try it over TCP. Also you can force to use only UDP or TCP.

Sipscan allows us to:
  * Identify SIP servers and devices.
  * Connect over UDP or TCP protocol.
  * Try UDP and TCP at the same time.
  * Use different methods like as REGISTER, INVITE or OPTIONS.
  * Scan for a server target or large ranges of network.
  * Scan for large ranges of ports.
  * Analyze responses using verbose mode.

# Usage #
```
$ perl sipscan.pl 

SipSCAN - by Pepelux <pepeluxx@gmail.com>
-------

Usage: perl sipscan.pl -h <host> [options]
 
== Options ==
-m <string>      = Method: REGISTER/INVITE/OPTIONS (default: OPTIONS)
-u  <string>     = Username
-s  <integer>    = Source number (CallerID) (default: 100)
-d  <integer>    = Destination number (default: 100)
-r  <integer>    = Remote port (default: 5060)
-proto  <string>  = Protocol (UDP or TCP - By default: UDP)
-ip <string>     = Source IP (by default it is the same as host)
-v               = Verbose (trace information)
-vv              = More verbose (more detailed trace)
```

  * To search SIP services on 192.168.0.1 port 5060 (using OPTIONS method)
```
$perl sipscan.pl -h 192.168.0.1
```
  * To search SIP services on 192.168.0.0 network (over TCP connection)
```
$perl sipscan.pl -h 192.168.0.0/24 -t tcp
```
  * To search a large range of SIP services (using REGISTER method)
```
$perl sipscan.pl -h 192.168.0.1-192.168.254.254 -m REGISTER
```
  * To search a large network range of SIP services on a large port range (using INVITE method)
```
$perl sipscan.pl -h 192.168.0.1-192.168.254.254 -r 5060-5090 -m INVITE
```

# Example #
```
$ perl sipscan.pl -h 192.168.0.0/24
[+] 192.168.0.51:5060 - Sending OPTIONS 100 => 100
[-] 401 Unauthorized
[+] 192.168.0.55:5060 - Sending OPTIONS 100 => 100
[-] 200 OK
[+] 192.168.0.54:5060 - Sending OPTIONS 100 => 100
[-] 483 Too Many Hops

IP:port			  User-Agent
=======			  ==========
192.168.0.51:5060/udp	| kamailio (4.2.1 (x86_64/linux))
192.168.0.54:5060/tcp	| kamailio (4.2.1 (x86_64/linux))
192.168.0.55:5060/udp	| Asterisk PBX 1.8.13.1~dfsg1-3+deb7u3
```