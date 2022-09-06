# recv_bbuf

### 설명

이더넷 객체로부터 바이너리 데이터를 수신하여 [BBuf](../../4-bbuf/README.md) 객체에 저장합니다.

### 문법

{ENet객체}.recv_bbuf {BBuf객체}\[,{대기시간}\]\[, {퇴피주소}\]



### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>BBuf객체</td>
      <td>
        수신한 바이너리 데이터를 전달받을 BBuf객체
      </td>
      <td></td>
    </tr>
    <tr>
      <td>대기시간</td>
      <td>
        timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행한다.<br>
        지정하지 않으면 무한 대기한다.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행한다.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>

### 리턴값

수신한 데이터 개수

### 사용 예

```python
var bbuf=enet_to_sensor.BBuf()
enet_to_sensor.recv bbuf
enet_to_sensor.recv bbuf, 5000
var nitem=enet_to_sensor.recv(bbuf,5000,*TimeOut)
end

*TimeOut
print "Time out! No response from sensor"
end
```

