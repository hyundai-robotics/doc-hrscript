# 6.2.1 생성자

### 설명

이더넷 객체를 생성합니다. 참조를 리턴합니다.

### 문법

ENet\(&lt;프로토콜&gt;\)

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
      <td style="text-align:left">&#xD504;&#xB85C;&#xD1A0;&#xCF5C;</td>
      <td style="text-align:left">
        <p>&quot;tcp&quot; : TCP &#xD1B5;&#xC2E0;
          <br />
        </p>
        <p>&quot;udp&quot; : UDP &#xD1B5;&#xC2E0;
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left">&#xC0DD;&#xB7B5;&#xD558;&#xBA74; &quot;udp&quot;&#xB85C; &#xC778;&#xC2DD;</td>
    </tr>
  </tbody>
</table>

### 리턴값

생성된 객체의 참조

### 사용 예

```python
enet0 = ENet()
var tcp = ENet("tcp")
```

티치펜던트의 \[기록\] 버튼을 누르면 현재로봇 자세로 숨은 포즈 방식의 move문이 기록됩니다. 숨은 포즈의 값은 move 문에 커서를 두고 \[속성\] 버튼을 눌러 확인하거나 편집할 수 있습니다.

