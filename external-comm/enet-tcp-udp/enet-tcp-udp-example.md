# 6.2.5 Examples of TCP and UDP Communication

```python
     import enet
     global msg
     global enet0=enet.ENet() # ENet("tcp") in case of TCP communication

     # port no. 49152–65535 contains dynamic or private ports
     enet0.ip_addr="192.168.1.172"
     enet0.lport=51001 # necessary only in case of UDP communication
     enet0.rport=51002

     enet0.open
     enet0.connect # necessary only in case of TCP communication
     print enet0.state() # normal if it is 1
     enet0.send "hello, "+"udp", 300, "\n"

     enet0.recv msg, 8000 # wait for 8 seconds
     print msg
     delay 1.5
     enet0.close
     print enet0.state() # normal if it is 0
     delay 1.5
     end

```

