# 5.4 move문

move문은 로봇을 움직이는 프로시져입니다. 형식은 아래와 같습니다.

### 설명

로봇의 툴 끝이 포즈 위치로 이동합니다.

### 문법

move &lt;보간&gt;, \[tg=&lt;포즈/시프트&gt;\], spd=&lt;속도&gt;, accu=&lt;정밀도&gt;

, tool=&lt;툴 번호&gt; \[until &lt;조건식&gt;\]

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
      <td style="text-align:left">&#xBCF4;&#xAC04;</td>
      <td style="text-align:left">
        <p>P : &#xCD95;&#xBCF4;&#xAC04;, L : &#xC9C1;&#xC120;&#xBCF4;&#xAC04;, C
          : &#xC6D0;&#xD638;&#xBCF4;&#xAC04;
          <br />
        </p>
        <p>SP: &#xC815;&#xCE58;&#xD234; &#xCD95;&#xBCF4;&#xAC04;, SL: &#xC815;&#xCE58;&#xD234;
          &#xC9C1;&#xC120;&#xBCF4;&#xAC04;,
          <br />
        </p>
        <p>SC: &#xC815;&#xCE58;&#xD234; &#xC6D0;&#xD638;&#xBCF4;&#xAC04;
          <br />
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&#xD3EC;&#xC988;/</p>
        <p>&#xC2DC;&#xD504;&#xD2B8;</p>
      </td>
      <td style="text-align:left">
        <p>&#xC774;&#xB3D9;&#xD560; &#xBAA9;&#xD45C;(target) &#xC790;&#xC138; (&#xD3EC;&#xC988;).
          <br
          />
        </p>
        <p>&#xC228;&#xC740; &#xD3EC;&#xC988;&#xAC00; &#xC788;&#xC73C;&#xBA74; &#xC0DD;&#xB7B5;&#xB429;&#xB2C8;&#xB2E4;.
          <br
          />
        </p>
        <p>+&#xB098; &#x2013; &#xBD80;&#xD638;&#xB97C; &#xBD99;&#xC778; &#xC2DC;&#xD504;&#xD2B8;&#xC2DD;&#xC744;
          &#xC9C0;&#xC815;&#xD558;&#xBA74; (&#xC228;&#xC740;&#xD3EC;&#xC988;+&#xC2DC;&#xD504;&#xD2B8;&#xC2DD;)&#xC774;
          &#xBAA9;&#xD45C; &#xC790;&#xC138;&#xB85C; &#xC801;&#xC6A9;&#xB429;&#xB2C8;&#xB2E4;.
          <br
          />
        </p>
      </td>
      <td style="text-align:left">
        <p>&#xD3EC;&#xC988;&#xC2DD;</p>
        <p>&#xD639;&#xC740;</p>
        <p>&#xBD80;&#xD638; &#xC2DC;&#xD504;&#xD2B8;&#xC2DD;
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#xC18D;&#xB3C4;</td>
      <td style="text-align:left">
        <p>&#xD234; &#xB05D;&#xC758; &#xC774;&#xB3D9;&#xC18D;&#xB3C4;.
          <br />
        </p>
        <p>&#xB2E8;&#xC704;(mm/sec, cm/min, sec, %)&#xB97C; &#xBD99;&#xC5EC;&#xC57C;
          &#xD569;&#xB2C8;&#xB2E4;.
          <br />
        </p>
      </td>
      <td style="text-align:left">&#xC0B0;&#xC220;&#xC2DD;.</td>
    </tr>
    <tr>
      <td style="text-align:left">&#xC815;&#xBC00;</td>
      <td style="text-align:left">&#xC0B0;&#xC220;&#xC2DD;. &#xB0AE;&#xC744;&#xC218;&#xB85D; &#xC815;&#xBC00;&#xD568;.
        0&#xC774;&#xBA74; &#xBD88;&#xC5F0;&#xC18D;&#xC73C;&#xB85C; &#xB3D9;&#xC791;</td>
      <td
      style="text-align:left">0~7</td>
    </tr>
    <tr>
      <td style="text-align:left">&#xD234; &#xBC88;&#xD638;</td>
      <td style="text-align:left">&#xB85C;&#xBD07; &#xB3D9;&#xC791; &#xC2DC; &#xC0AC;&#xC6A9;&#xD560; &#xD234;&#xC758;
        &#xBC88;&#xD638;.</td>
      <td style="text-align:left">0~31</td>
    </tr>
    <tr>
      <td style="text-align:left">&#xC870;&#xAC74;&#xC2DD;</td>
      <td style="text-align:left">
        <p>&#xC870;&#xAC74;&#xC2DD;&#xC774; &#xCC38;&#xC778; &#xC21C;&#xAC04; &#xB85C;&#xBD07;&#xB3D9;&#xC791;&#xC774;
          &#xC885;&#xB8CC;&#xB418;&#xACE0; &#xC9C0;&#xC815;&#xD55C; &#xD3EC;&#xC988;&#xC5D0;
          &#xB3C4;&#xB2EC;&#xD55C; &#xAC83;&#xC73C;&#xB85C; &#xAC04;&#xC8FC;&#xD569;&#xB2C8;&#xB2E4;.
          <br
          />
        </p>
        <p>&#xC870;&#xAC74;&#xC2DD;&#xC758; &#xACB0;&#xACFC;&#xB294; result( ) &#xD568;&#xC218;&#xB85C;
          &#xC5BB;&#xC744; &#xC218; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>0&#xC774; &#xC544;&#xB2C8;&#xBA74; &#xCC38;
          <br />
        </p>
        <p>0&#xC774;&#xBA74; &#xAC70;&#xC9D3;
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
move L,tg=po[0]+sft[1],spd=800mm/sec,accu=0,tool=1
move P,tg=+Shift(0,0,0,0,-10,0),spd=80%,accu=1,tool=3 until di2  (숨은 포즈)
if result() then *sensor_on
```

티치펜던트의 \[기록\] 버튼을 누르면 현재로봇 자세로 숨은 포즈 방식의 move문이 기록됩니다. 숨은 포즈의 값은 move 문에 커서를 두고 \[속성\] 버튼을 눌러 확인하거나 편집할 수 있습니다.

\[명령입력\] 버튼을 누르고 \[모션\] 그룹을 연 후 move 메뉴를 선택하면, 포즈 방식의 move문이 기록됩니다.



