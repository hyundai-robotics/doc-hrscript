# recv

### 설명

설정된 이더넷 객체로 값들을 수신합니다.

### 문법

&lt;ENet객체&gt;.recv &lt;변수&gt;\[, &lt;대기시간&gt;\]



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
      <td style="text-align:left">변수</td>
      <td style="text-align:left">수신된 문자열을 전달받을
        변수</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">대기시간</td>
      <td style="text-align:left">
        <p>timeout 시간. 경과하면 다음
          명령문으로 진행한다.
          <br
          />
        </p>
        <p>지정하지 않으면 무한
          대기한다.
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left">msec</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
enet_to_sensor.recv  msg, 5000
```

