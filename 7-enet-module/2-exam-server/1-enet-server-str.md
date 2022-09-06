# 7.2.1 ethernet TCP server - 문자열 송수신

다음과 같은 순서로 수행합니다.

1. enet 모듈 import 후, 생성자로 ENet 객체 생성.
2. 멤버변수로 IP주소와 port번호를 설정. (remote port 설정은 필요없음.)
3. open 멤버 프로시져로 ethernet socket 열고, listen(), accept() 함수를 수행함. state\(\) 멤버변수로 상태 확인.
4. send, recv 멤버 프로시져로 송수신 수행.
5. close 멤버 프로시져로 통신 연결 닫기.


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
     
     # --------------------------------
     # 4-1. string 송신
     svr.send "Welcome, I am a TCP server.\n"
     
     # 4-2. string 수신
     #     (5초간 수신 없으면 *TimeOut 레이블로 jump)
     svr.recv 5000,*TimeOut
     var msg=result() # 수신된 문자열
     print msg
     delay 1.0
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
