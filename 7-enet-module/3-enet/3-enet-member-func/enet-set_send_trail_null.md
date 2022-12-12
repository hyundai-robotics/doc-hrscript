# set_send_trail_null

### 설명

`ENet.send()` 함수로 문자열을 송신할 때, 종료 null문자(terminating-null)를 붙여서 송신할 지 여부를 설정합니다. (default는 false)

### 문법

`{ENet객체}.set_send_trail_null(true|false)`


### 리턴값

없음.


### 사용 예

```python
enet_to_sensor.set_send_trail_null(true)
enet_to_sensor.send "ACK"
enet_to_sensor.set_send_trail_null(false)
```
