# 6.2 enet 모듈 : 이더넷 TCP/UDP 통신

Hi6 제어기의 범용 이더넷 포트를 통해, 외부 장치와 이더넷 TCP 혹은 UDP 통신으로 문자열 송수신을 할 수 있습니다.

이 기능을 사용하기 위해서는 아래와 같이 enet 모듈을 import한 후, ENet 객체를 생성해야 합니다.

```python
import enet
var udp=enet.ENet("udp")
```

ENet 생성자의 파라미터로서 아래와 같이 "udp" 혹은 "tcp"를 전달하여 프로토콜을 선택해야 합니다. default는 "udp"이므로, UDP 통신을 할 때는 아래와 같이 생략해도 됩니다.

```python
var udp=enet.ENet()
```

다음과 같은 순서로 통신을 수행합니다.

1. 생성자로 ENet 객체 생성
2. 멤버변수로 IP주소와 포트번호를 설정
3. open 멤버 프로시져로 통신 연결 열고, state\(\) 멤버변수로 상태 확인 \(TCP통신인 경우에는 open 후 connect 프로시져도 수행해야 함.\)
4. send, recv 멤버 프로시져로 송수신 수행
5. close 멤버 프로시져로 통신 연결 닫기









