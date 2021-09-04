# 6.4.1 input문

### 설명

input문을 통해 티치펜던트의 키입력으로 문자열을 입력받아 변수에 저장합니다. 제한시간까지 입력되지 않으면 다음 명령문으로 진행하거나 timeout 주소로 분기합니다.

### 문법

input &lt;변수&gt;\[,&lt;제한시간&gt;,&lt;timeout 주소&gt;\]



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
      <td style="text-align:left">
        <p>&#xC785;&#xB825;&#xC744; &#xBC1B;&#xC744; &#xBCC0;&#xC218;. &#xC22B;&#xC790;&#xB3C4;
          &#xBB38;&#xC790;&#xC5F4; &#xD0C0;&#xC785;&#xC73C;&#xB85C; &#xC785;&#xB825;&#xBC1B;&#xC2B5;&#xB2C8;&#xB2E4;.
          &#xC218;&#xCE58;&#xAC12;&#xC774; &#xD544;&#xC694;&#xD558;&#xBA74; int(
          )&#xB098; double( ) &#xD568;&#xC218;&#xB85C; &#xBCC0;&#xD658;&#xD558;&#xC2ED;&#xC2DC;&#xC624;.
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
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#xC81C;&#xD55C;&#xC2DC;&#xC0B0;</td>
      <td style="text-align:left">&#xC785;&#xB825;&#xC744; &#xB300;&#xAE30;&#xD560; &#xCD5C;&#xB300; &#xC81C;&#xD55C;
        &#xC2DC;&#xAC04; (timeout)</td>
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

```python
input work_no
input work_no,10
input work_no,10,*timeout
```

![](../../.gitbook/assets/image%20%286%29.png)



