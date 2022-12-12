# 7.1.2 peer-to-peer, client Example - Transceiving binary data

Binary transceiving are performed using `BBuf` (binary buffer) object.  
(Only the transceiving parts are different, and the rest are the same as the transceiving string data.)

Sending

1. Create `enet.BBuf` object.
2. Append the desired binary data to the `BBuf` object with the `BBuf.append()` function.
3. Send the BBuf object as a function of `ENET.send_bbuf()`


Receiving

1. Create `enet.BBuf` object.
2. Receive binary data into BBuf objects with the `ENET.recv_bbuf()` function.
3. Read the desired binary data from the `BBuf` object with the `BBuf.read_nums()` function.


<br>

### UDP peer-to-peer
```python
     # 1. After importing the enet module, create an ENet object with the constructor
     import enet
     var cli=enet.ENet() # For TCP communications, ENet("tcp")

     # 2. Set the IP address and port number
     cli.ip_addr="192.168.1.172" # remote (opponent) IP address
     cli.lport=51001 # local (self) port
     cli.rport=51002 # remote (opponent) port
     # (port no. 49152–65535 contains dynamic or private ports)

     # 3. Open ethernet socket
     cli.open
     
     print cli.state() # If 1, it's OK.

     # Sending --------------------------------
     # 4-1. Create BBuf object
     var bbuf=enet.BBuf()

     # (sample binary data)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. Append binary data to BBuf object
     bbuf.clear()
     bbuf.append("s4", arr) # append little endian signed-4byte data

     # 4-3. Send BBuf object
     var ret
     ret=cli.send_bbuf(bbuf)

     # Receiving --------------------------------
     # 4-1. Create BBuf object
     var bbuf2=enet.BBuf()
     
     # 4-2. Receive binary data into BBuf object
     #     (If no response for 3 seconds, jump to *TimeOut label)
     cli.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. Read binary data from BBuf object.
     var nums=bbuf2.read_nums("U2", 0, 3) # read 3 big-endian unsigned-2byte data
     print nums
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


### TCP client
(Only `lport` and `connect` parts are different from peer-to-peer.)
```python
     # 1. After importing the enet module, create an ENet object with the constructor
     import enet
     var cli=enet.ENet() # For TCP communications, ENet("tcp")

     # 2. Set the IP address and port number
     cli.ip_addr="192.168.1.172" # remote (opponent) IP address
     cli.lport=0 # local (self) port; random
     cli.rport=51002 # remote (opponent) port
     # (port no. 49152–65535 contains dynamic or private ports)

     # 3. Open ethernet socket
     cli.open
     cli.connect # connect to the server.
     print cli.state() # If 1, it's OK.

     # Sending --------------------------------
     # 4-1. Create BBuf object
     var bbuf=enet.BBuf()

     # (sample binary data)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. Append binary data to BBuf object
     bbuf.clear()
     bbuf.append("s4", arr) # append little endian signed-4byte data

     # 4-3. Send BBuf object
     var ret
     ret=cli.send_bbuf(bbuf)

     # Receiving --------------------------------
     # 4-1. Create BBuf object
     var bbuf2=enet.BBuf()
     
     # 4-2. Receive binary data into BBuf object
     #     (If no response for 3 seconds, jump to *TimeOut label)
     cli.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. Read binary data from BBuf object.
     var nums=bbuf2.read_nums("U2", 0, 3) # read 3 big-endian unsigned-2byte data
     print nums
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

* String arguments such as "s4" and "U2" determine the binary data format such as endian type, signed/unsigned, and the number of bytes. For more information, see [7.4.2 Supported format](../4-bbuf/2-format.md).