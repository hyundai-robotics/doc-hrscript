# 6.2.5 TCP, UDP 통신 예제

```python
     import enet
     global msg
     global enet0=enet.ENet() # TCP 통신인 경우, ENet("tcp")

     # port no. 49152–65535 contains dynamic or private ports
     enet0.ip_addr="192.168.1.172"
     enet0.lport=51001 # UDP 통신에서만 필요
     enet0.rport=51002

     enet0.open
     enet0.connect # TCP 통신에서만 필요
     print enet0.state() # 1이면 정상
     enet0.send "hello, "+"udp", 300, "\n"

     enet0.recv msg, 8000 # 8초간 대기
     print msg
     delay 1.5
     enet0.close
     print enet0.state() # 0이면 정상
     delay 1.5
     end
```

