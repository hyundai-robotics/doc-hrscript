# 3.2.4 wait문

### 설명

지정한 조건이 참이 될 때까지 대기한 후 다음 명령문으로 진행합니다.

### 문법

wait &lt;조건&gt;\[,&lt;제한시간&gt;,\]

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
      <td style="text-align:left">&#xC870;&#xAC74;</td>
      <td style="text-align:left">&#xB300;&#xAE30;&#xD560; &#xC870;&#xAC74;</td>
      <td style="text-align:left">&#xC870;&#xAC74;&#xC2DD;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#xC81C;&#xD55C;&#xC2DC;&#xAC04;</td>
      <td style="text-align:left">&#xC870;&#xAC74;&#xC774; &#xAC70;&#xC9D3;&#xC77C; &#xACBD;&#xC6B0; &#xB300;&#xAE30;&#xD560;
        &#xCD5C;&#xB300; &#xC81C;&#xD55C; &#xC2DC;&#xAC04; (timeout)</td>
      <td style="text-align:left">
        <p>&#xC0B0;&#xC220;&#xC2DD;
          <br />
        </p>
        <p>0.1~60.0 sec
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">timeout &#xC8FC;&#xC18C;</td>
      <td style="text-align:left">&#xC81C;&#xD55C;&#xC2DC;&#xAC04; &#xCD08;&#xACFC; &#xC2DC;, &#xBD84;&#xAE30;&#xD560;
        &#xC8FC;&#xC18C;</td>
      <td style="text-align:left">&#xC8FC;&#xC18C;</td>
    </tr>
  </tbody>
</table>

### 사용 예

```javascript
wait sensor_ok
wait (sensor_ok and pos_ok),10,*timeout
```

