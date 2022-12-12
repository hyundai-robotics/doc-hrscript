# 7.1.1 peer-to-peer, client 예제 - 문자열 송수신

다음과 같은 순서로 수행합니다.

1. `enet` 모듈 import 후, 생성자로 `ENet` 객체 생성.
2. 멤버변수로 IP주소와 port번호를 설정.
3. `open` 멤버 프로시져로 ethernet socket 열고, `state()` 멤버변수로 상태 확인.  
\(TCP통신인 경우에는 `open` 후 `connect` 프로시져도 수행해야 함.\)
4. `send`, `recv` 멤버 프로시져로 송수신 수행.
5. `close` 멤버 프로시져로 통신 연결 닫기.

<br>

### UDP peer-to-peer
```python
     # 1. enet 모듈 import 후, 생성자로 ENet 객체 생성
     import enet
     var cli=enet.ENet() # TCP 통신인 경우, ENet("tcp")

     # 2. IP주소와 port번호 설정
     cli.ip_addr="192.168.1.172" # remote (상대방) IP address
     cli.lport=51001 # local (자신) port
     cli.rport=51002 # remote (상대방) port 
     # (port no. 49152–65535 contains dynamic or private ports)

     # 3. ethernet socket 열기
     cli.open

     print cli.state() # 1이면 정상

     # --------------------------------
     # 4-1. string 송신
     cli.send "hello, peer.\n"

     # 4-2. string 수신
     #     (5초간 수신 없으면 *TimeOut 레이블로 jump)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # 수신된 문자열
     print msg
     delay 1.0
     # --------------------------------

     # 5. ethernet socket 닫기
     cli.close
     print cli.state() # 0이면 정상
     delay 1.5
     end

     *TimeOut
     print "time out!"
     cli.close
     end
```
<br>

### TCP client
(peer-to-peer와는 `lport`와 `connect` 부분만 다름.)
```python
     # 1. enet 모듈 import 후, 생성자로 ENet 객체 생성
     import enet
     var cli=enet.ENet() # TCP 통신인 경우, ENet("tcp")

     # 2. IP주소와 port번호 설정
     cli.ip_addr="192.168.1.172" # remote (상대방) IP address
     cli.lport=0 # local (자신) port; 무작위
     cli.rport=51002 # remote (상대방) port 
     # (port no. 49152–65535 contains dynamic or private ports)

     # 3. ethernet socket 열기
     cli.open
     cli.connect # 서버에 접속.
     print cli.state() # 1이면 정상

     # --------------------------------
     # 4-1. string 송신
     cli.send "hello, peer.\n"

     # 4-2. string 수신
     #     (5초간 수신 없으면 *TimeOut 레이블로 jump)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # 수신된 문자열
     print msg
     delay 1.0
     # --------------------------------

     # 5. ethernet socket 닫기
     cli.close
     print cli.state() # 0이면 정상
     delay 1.5
     end

     *TimeOut
     print "time out!"
     cli.close
     end
```