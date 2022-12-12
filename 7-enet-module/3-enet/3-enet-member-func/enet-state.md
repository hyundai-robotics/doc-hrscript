# state

### 설명

이더넷 객체의 상태를 리턴합니다.

### 문법

`{ENet객체}.state`



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
        연결됨. <br>
        (UDP일 때는 `open`만 해도 연결로 간주됩니다.<br>
        TCP일 때는 `open` 후 `listen`, `connect`, `accept`도 수행되어야 연결로 간주됩니다.)
      </td>
      <td></td>
    </tr>
    <tr>
      <td>0</td>
      <td>연결 안됨.</td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>이더넷소켓 생성 실패</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>이더넷장치 BIND 실패</td>
      <td></td>
    </tr>
    <tr>
      <td>-3</td>
      <td>connect 실패</td>
      <td></td>
    </tr>
    <tr>
      <td>-4</td>
      <td>listen 실패</td>
      <td></td>
    </tr>
    <tr>
      <td>-5</td>
      <td>accept 실패</td>
      <td></td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
var ret = enet_to_sensor.state()
```

