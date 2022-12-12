# listen

### 설명

이더넷 TCP 통신에서 server로서 client의 연결을 준비합니다.  
UDP peer-to-peer 통신에서는 사용되지 않습니다.

### 문법

`{ENet객체}.listen [{backlog}]`

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
      <td>backlog</td>
      <td>
        accept 되지 않은 연결의 허용 개수<br>
        지정하지 않으면 적절한 값이 선택됩니다.
      </td>
      <td></td>
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
      <td>0</td>
      <td>
        성공
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>에러</td>
      <td></td>
    </tr>	 
  </tbody>
</table>


### 사용 예

```python
enet_to_sensor.listen
enet_to_sensor.accept 5000,*TimeOut
```
