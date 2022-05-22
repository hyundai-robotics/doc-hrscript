# 6.2    ENet Module: Ethernet TCP/UDP Communication

Using the general-purpose Ethernet port of the Hi6 Controller makes it possible to transmit or receive a string with an external device through Ethernet TCP or UDP communication. It is required to create an ENet object after importing the ENet module to use this function, as shown below.

```python
import enet
var udp=enet.ENet("udp")
```

In the following example, the selection of protocol is needed by passing "udp" or "tcp" as a parameter of the ENet constructor. The default is "udp," so like in the example, it can be omitted when UDP communication is performed.

```python
var udp=enet.ENet()
```

Communication must be performed in the following order:

1. Create an ENet object with the constructor.
2. Set an IP address and port number with the member variable.
3. Open the communication connection with the open member procedure, and check the state with the state\(\) member variable.

   \(In the case of TCP communication, the connect procedure should also be performed after opening\).

4. Perform transmission/reception with the send and receive member procedures.
5. Close the communication connection with the close member procedure.









