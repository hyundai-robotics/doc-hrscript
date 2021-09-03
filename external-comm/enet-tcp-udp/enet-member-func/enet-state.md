# state

### 설명

이더넷 객체의 상태를 리턴합니다.

### 문법

&lt;ENet객체&gt;.state\(\)



### 리턴값

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xAC12;</th>
      <th style="text-align:left">&#xC758;&#xBBF8;</th>
      <th style="text-align:left">&#xAE30;&#xD0C0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">
        <p>&#xC5F0;&#xACB0;&#xB428;.
          <br />
        </p>
        <p>(UDP&#xC77C; &#xB54C;&#xB294; open&#xB9CC; &#xD574;&#xB3C4; &#xC5F0;&#xACB0;&#xB85C;
          &#xAC04;&#xC8FC;&#xB429;&#xB2C8;&#xB2E4;. TCP&#xC77C; &#xB54C;&#xB294;
          open &#xD6C4; connect&#xB3C4; &#xC218;&#xD589;&#xD574;&#xC57C; &#xC5F0;&#xACB0;&#xB85C;
          &#xAC04;&#xC8FC;&#xB429;&#xB2C8;&#xB2E4;.)
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
      <td style="text-align:left">&#xC5F0;&#xACB0; &#xC548;&#xB428;.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">-1</td>
      <td style="text-align:left">&#xC774;&#xB354;&#xB137;&#xC18C;&#xCF13; &#xC0DD;&#xC131; &#xC2E4;&#xD328;</td>
      <td
      style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">-2</td>
      <td style="text-align:left">&#xC774;&#xB354;&#xB137;&#xC7A5;&#xCE58; BIND &#xC2E4;&#xD328;</td>
      <td
      style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
ret = enet_to_sensor.state()
```

