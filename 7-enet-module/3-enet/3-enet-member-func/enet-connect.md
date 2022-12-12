# connect

### 설명

이더넷 TCP 통신에서 client로서 server에 연결을 시도합니다.  
UDP peer-to-peer 통신에서는 사용되지 않습니다.

### 문법

`{ENet객체}.connect [{대기시간}] [, {퇴피주소}]`


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
      <td>대기시간</td>
      <td>
        timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행.<br>
        지정하지 않으면 무한 대기.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>


### 리턴값

<table>
  <thead>
    <tr>
      <th style="text-align:left">값</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>
        성공
      </td>
      <td></td>
    </tr>  
    <tr>
      <td>0</td>
      <td>
        대기 중
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>timeout</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>error</td>
      <td></td>
    </tr>
  </tbody>
</table>


### 사용 예

```python
var ret=enet_to_sensor.connect(5000)
```

```python
enet_to_sensor.connect 5000,*TimeOut
```