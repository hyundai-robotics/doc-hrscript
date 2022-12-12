# 7.1.1 peer-to-peer, client Example - Transceiving string data

Follow these steps:

1. After importing the `enet` module, create an `ENet` object with the constructor.
2. Set the IP address and port number with the member variables.
3. Open the ethernet socket with the `open` member procedure, and check the status with the `state()` member variable.
\(For TCP communication, the `connect` procedure must also be called after opening.\)
4. Transceiving with `send` and `recv` member procedure.
5. Close the communication connection with the `close` member procedure.

<br>

### UDP peer-to-peer
```python
     # 1. After importing the enet module, create an ENet object with the constructor
     import enet
     var cli=enet.ENet() # for TCP communication, ENet("tcp")

     # 2. Set the IP address and port number
     cli.ip_addr="192.168.1.172" # remote (opponent) IP address
     cli.lport=51001 # local (self) port
     cli.rport=51002 # remote (opponent) port
     # (port no. 49152–65535 contains dynamic or private ports)

     # 3. Open ethernet socket
     cli.open
     
     print cli.state() # If 1, it's OK.

     # --------------------------------
     # 4-1. string trasmitting
     cli.send "hello, peer.\n"

     # 4-2. string receiving
     #     (if not received for 5 seconds, jump to *TimeOut label)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # received string
     print msg
     delay 1.0
     # --------------------------------

     # 5. Close ethernet socket
     cli.close
     print cli.state() # If 0, it's OK.
     delay 1.5
     end

     *TimeOut
     print "time out!"
     cli.close
     end
```
<br>

### TCP client
(Only `lport` and `connect` parts are different from peer-to-peer.)
```python
     # 1. After importing the enet module, create an ENet object with the constructor
     import enet
     var cli=enet.ENet() # for TCP communication, ENet("tcp")

     # 2. Set the IP address and port number
     cli.ip_addr="192.168.1.172" # remote (opponent) IP address
     cli.lport=0 # local (self) port; random
     cli.rport=51002 # remote (opponent) port
     # (port no. 49152–65535 contains dynamic or private ports)

     # 3. Open ethernet socket
     cli.open
     cli.connect # connect to the server.
     print cli.state() # If 1, it's OK.

     # --------------------------------
     # 4-1. string trasmitting
     cli.send "hello, peer.\n"

     # 4-2. string receiving
     #     (if not received for 5 seconds, jump to *TimeOut label)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # received string
     print msg
     delay 1.0
     # --------------------------------

     # 5. Close ethernet socket
     cli.close
     print cli.state() # If 0, it's OK.
     delay 1.5
     end

     *TimeOut
     print "time out!"
     cli.close
     end
```
