# state

### 설명

이더넷 객체의 상태를 리턴합니다.

### 문법

&lt;ENet객체&gt;.state\(\)



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
      <td style="text-align:left">1</td>
      <td style="text-align:left">
        <p>연결됨.
          <br />
        </p>
        <p>(UDP일 때는 open만 해도 연결로
          간주됩니다. TCP일 때는
          open 후 connect도 수행해야 연결로
          간주됩니다.)
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
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">0</td>
      <td style="text-align:left">연결 안됨.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">-1</td>
      <td style="text-align:left">이더넷소켓 생성 실패</td>
      <td
      style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">-2</td>
      <td style="text-align:left">이더넷장치 BIND 실패</td>
      <td
      style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
ret = enet_to_sensor.state()
```

