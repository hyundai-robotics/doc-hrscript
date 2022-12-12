# 7.2.1 ethernet TCP server - Transceiving string data

Follow these steps:

1. After importing the `enet` module, create an `ENet` object with the constructor.
2. Set the IP address and port number with the member variables. (remote port setting is not needed.)
3. Open the ethernet socket with the `open` member procedure, and calls `listen()`, `accept()` function. Check the status with the `state()` member variable.
4. Transceiving with `send` and `recv` member procedure.
5. Close the communication connection with the `close` member procedure.


```python
     # 1. After importing the enet module, create an ENet object with the constructor
     import enet
     var svr=enet.ENet("tcp")
     
     # 2. Set the IP address and port number
     svr.ip_addr="192.168.1.172" # remote (opponent) IP address
     svr.lport=51001 # local (self) port
     # (port no. 49152–65535 contains dynamic or private ports)
     
     # 3. Open ethernet socket
     svr.open
     var ret
     ret=svr.listen()
     ret=svr.accept() # wait for connect from client
     print svr.state() # If 1, it's OK.
     
     # --------------------------------
     # 4-1. string trasmitting
     svr.send "Welcome, I am a TCP server.\n"
     
     # 4-2. string receiving
     #     (if not received for 5 seconds, jump to *TimeOut label)
     svr.recv 5000,*TimeOut
     var msg=result() # received string
     print msg
     delay 1.0
     # --------------------------------
     
     # 5. Close ethernet socket
     svr.close
     print svr.state() # If 0, it's OK.
     delay 1.5
     end

     *TimeOut
     print "time out!"
     svr.close
     end
```
