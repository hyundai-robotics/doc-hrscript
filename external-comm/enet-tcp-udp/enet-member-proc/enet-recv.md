# recv

### 설명

설정된 이더넷 객체로 값들을 수신합니다.

### 문법

&lt;ENet객체&gt;.recv &lt;변수&gt;\[, &lt;대기시간&gt;\]



### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xD56D;&#xBAA9;</th>
      <th style="text-align:left">&#xC758;&#xBBF8;</th>
      <th style="text-align:left">&#xAE30;&#xD0C0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#xBCC0;&#xC218;</td>
      <td style="text-align:left">&#xC218;&#xC2E0;&#xB41C; &#xBB38;&#xC790;&#xC5F4;&#xC744; &#xC804;&#xB2EC;&#xBC1B;&#xC744;
        &#xBCC0;&#xC218;</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#xB300;&#xAE30;&#xC2DC;&#xAC04;</td>
      <td style="text-align:left">
        <p>timeout &#xC2DC;&#xAC04;. &#xACBD;&#xACFC;&#xD558;&#xBA74; &#xB2E4;&#xC74C;
          &#xBA85;&#xB839;&#xBB38;&#xC73C;&#xB85C; &#xC9C4;&#xD589;&#xD55C;&#xB2E4;.
          <br
          />
        </p>
        <p>&#xC9C0;&#xC815;&#xD558;&#xC9C0; &#xC54A;&#xC73C;&#xBA74; &#xBB34;&#xD55C;
          &#xB300;&#xAE30;&#xD55C;&#xB2E4;.
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

