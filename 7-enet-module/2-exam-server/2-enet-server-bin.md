# 7.2.2 ethernet TCP server 예제 - 바이너리 송수신

바이너리 송수신은 BBuf (Binary Buffer) 객체를 통해 수행합니다.  
(송수신 부분만 다르고, 나머지는 문자열 송수신과 동일합니다.)

송신

1. `enet.BBuf` 객체 생성.
2. 원하는 바이너리 데이터를 `BBuf.append()` 함수로 `BBuf` 객체에 추가.
3. `ENet.send_bbuf()` 함수로 BBuf 객체를 송신.


수신

1. `enet.BBuf` 객체 생성.
2. `ENet.recv_bbuf()` 함수로 `BBuf` 객체에 바이너리 데이터를 수신
3. 원하는 바이너리 데이터를 `BBuf.read_nums()` 함수로 `BBuf` 객체로부터 읽기.


```python
     # 1. enet 모듈 import 후, 생성자로 ENet 객체 생성
     import enet
     var svr=enet.ENet("tcp")
     
     # 2. IP주소와 port번호 설정
     svr.ip_addr="192.168.1.172" # remote (상대방) IP address
     svr.lport=51001 # local (자신) port
     # (port no. 49152–65535 contains dynamic or private ports)
     
     # 3. ethernet socket 열기
     svr.open
     var ret
     ret=svr.listen()
     ret=svr.accept() # client로부터의 connect 대기
     print svr.state() # 1이면 정상

     # 송신 --------------------------------
     # 4-1. BBuf 객체 생성
     var bbuf=enet.BBuf()

     # (sample binary data)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. binary data를 BBuf 객체에 추가.
     bbuf.clear()
     bbuf.append("s4", arr) # little endian signed-4byte data 추가

     # 4-3. BBuf 객체를 송신
     ret=svr.send_bbuf(bbuf)

     # 수신 --------------------------------
     # 4-1. BBuf 객체 생성
     var bbuf2=enet.BBuf()
     
     # 4-2. BBuf 객체에 binary data를 수신
     #     (3초간 수신 없으면 *TimeOut 레이블로 jump)
     svr.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. binary data를 BBuf 객체로부터 읽기.
     var nums=bbuf2.read_nums("U2", 0, 3) # big-endian unsigned-2byte data 3개 읽기
     print nums
     # --------------------------------

     # 5. ethernet socket 닫기
     svr.close
     print svr.state() # 0이면 정상
     delay 1.5
     end

     *TimeOut
     print "time out!"
     svr.close
     end
```

* "s4"나 "U2" 같은 문자열 인수가 endian 방식, signed/unsigned, byte수 같은 binary data 형식을 결정합니다. 자세한 내용은 [7.4.2 지원 형식 (format)](../4-bbuf/2-format.md)을 참조하십시오.
