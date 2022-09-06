# accept

### 설명

이더넷 TCP 통신에서 server로서 client측의 연결 요청이 올 때까지 기다립니다. 요청이 발생하면 연결을 만듭니다.  
UDP peer-to-peer 통신에서는 사용되지 않습니다.

### 문법

{ENet객체}.accept

### 사용 예

```python
enet_to_sensor.listen
enet_to_sensor.accept
```

