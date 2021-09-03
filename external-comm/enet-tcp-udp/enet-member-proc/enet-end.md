# send

### 설명

설정된 이더넷 객체로 값들을 송신합니다.

### 문법

&lt;ENet객체&gt;.send &lt;값&gt;, &lt;값&gt;, …



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
      <td style="text-align:left">&#xAC12;</td>
      <td style="text-align:left">
        <p>&#xCD9C;&#xB825;&#xD560; &#xB370;&#xC774;&#xD130; &#xAC12;.
          <br />
        </p>
        <p>&#xC27C;&#xD45C;&#xB85C; &#xBD84;&#xB9AC;&#xB41C; &#xC778;&#xC218;&#xB4E4;&#xC740;
          &#xACF5;&#xBC31;&#xC73C;&#xB85C; &#xB098;&#xB258;&#xC5B4; &#xCD9C;&#xB825;.
          <br
          />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left">&#xBAA8;&#xB4E0; &#xB370;&#xC774;&#xD130;&#xD615;</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
enet_to_sensor.send "rob:", 10, ", command:"+cmd, "\n"
```



