# 5.4 move문

move문은 로봇을 움직이는 프로시져입니다. 형식은 아래와 같습니다.

### 설명

로봇의 툴 끝이 포즈 위치로 이동합니다.

### 문법

move &lt;보간&gt;, \[tg=&lt;포즈/시프트&gt;\], spd=&lt;속도&gt;, accu=&lt;정밀도&gt;

, tool=&lt;툴 번호&gt; \[x=&lt;대입문&gt;,\] \[until &lt;조건식&gt;\]

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
      <td style="text-align:left">보간</td>
      <td style="text-align:left">
        <p>P : 축보간, L : 직선보간, C
          : 원호보간
          <br />
        </p>
        <p>SP: 정치툴 축보간, SL: 정치툴
          직선보간,
          <br />
        </p>
        <p>SC: 정치툴 원호보간
          <br />
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>포즈/</p>
        <p>시프트</p>
      </td>
      <td style="text-align:left">
        <p>이동할 목표(target) 자세 (포즈).
          <br
          />
        </p>
        <p>숨은 포즈가 있으면 생략됩니다.
          <br
          />
        </p>
        <p>+나 - 부호를 붙인 시프트식을
          지정하면 (숨은포즈+시프트식)이
          목표 자세로 적용됩니다.
          <br
          />
        </p>
      </td>
      <td style="text-align:left">
        <p>포즈식</p>
        <p>혹은</p>
        <p>부호 시프트식
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">속도</td>
      <td style="text-align:left">
        <p>툴 끝의 이동속도.
          <br />
        </p>
        <p>단위(mm/sec, cm/min, sec, %)를 붙여야
          합니다.
          <br />
        </p>
      </td>
      <td style="text-align:left">산술식.</td>
    </tr>
    <tr>
      <td style="text-align:left">정밀도</td>
      <td style="text-align:left">산술식. 낮을수록 정밀함.
        0이면 불연속으로 동작</td>
      <td
      style="text-align:left">0~7</td>
    </tr>
    <tr>
      <td style="text-align:left">툴 번호</td>
      <td style="text-align:left">로봇 동작 시 사용할 툴의
        번호.</td>
      <td style="text-align:left">0~31</td>
    </tr>
    <tr>
      <td style="text-align:left">대입문</td>
      <td style="text-align:left">
        <p>move 출발 시, 수행 할 대입문
          <br
          />
        </p>
        <p>왼쪽부터 순차적으로 각 대입문이 수행됩니다.
          <br
          />
        </p>
      </td>
      <td style="text-align:left">
      "&lt;대입문1;대입문2;...&gt;"
      </td>
    </tr>
    <tr>
      <td style="text-align:left">조건식</td>
      <td style="text-align:left">
        <p>조건식이 참인 순간 로봇동작이
          종료되고 지정한 포즈에
          도달한 것으로 간주합니다.
          <br
          />
        </p>
        <p>조건식의 결과는 result( ) 함수로
          얻을 수 있습니다.
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>0이 아니면 참
          <br />
        </p>
        <p>0이면 거짓
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
move L,tg=po[0]+sft[1],spd=800mm/sec,accu=0,tool=1
move P,tg=+Shift(0,0,0,0,-10,0),spd=80%,accu=1,tool=3, x="do1=1;do2=2", until di2  (숨은 포즈)
if result() then *sensor_on
```

티치펜던트의 \[기록\] 버튼을 누르면 현재로봇 자세로 숨은 포즈 방식의 move문이 기록됩니다. 숨은 포즈의 값은 move 문에 커서를 두고 \[속성\] 버튼을 눌러 확인하거나 편집할 수 있습니다.

\[명령입력\] 버튼을 누르고 \[모션\] 그룹을 연 후 move 메뉴를 선택하면, 포즈 방식의 move문이 기록됩니다.


원호 보간(C, SC)의 동작 특성 및 예외 처리
원(Circle)을 정의하기 위해서는 최소 3개의 점이 필요하므로, 원호 보간 명령은 현재 위치를 기준으로 참조 위치(경유점)와 목표 위치(종점)가 순차적으로 필요합니다. 이에 따라 자사 사양에서는 다음과 같은 예외 및 개선 규칙을 적용합니다.

1. 마지막 스텝의 예외 처리 (정상 원호 보간)
프로그램의 마지막 스텝이 원호 보간으로 끝나는 경우, 예외적으로 정상적인 원호 궤적을 그리며 동작합니다.
```python
# [예시 1] 정상 동작
move C,tg=p0,spd=100%,accu=1,tool=1
move C,tg=p1,spd=100%,accu=1,tool=1 // 원호 보간 수행
end
```

2. 불연속 명령어에 따른 직선 보간 처리 (주의 요망)
원호 보간 뒤에 불연속 명령어(stop, delay 등)가 오고, 해당 스텝이 프로그램의 마지막 스텝이 아닌 경우에는 경유점까지의 궤적이 불연속 처리되어 직선 보간으로 수행됩니다.
```python
# [예시 2] 불연속 명령어로 인해 직선 보간
move C,tg=p0,spd=100%,accu=1,tool=1
move C,tg=p1,spd=100%,accu=1,tool=1 // 직선 보간 수행
stop
move C,tg=p2,spd=100%,accu=1,tool=1
move C,tg=p3,spd=100%,accu=1,tool=1 // 원호 보간 수행
end
```

3. 예시 2의 개선 방안
불연속 명령어 직전에 의도한 원호 궤적을 완전히 보장하려면, 아래와 같이 stop 실행 전에 목표 위치(p1)까지 축보간(P) 또는 직선보간(L) 등으로 명확히 도달 처리해 주는 것이 좋습니다.
```python
# [예시 2 개선] 원호 보간 궤적을 정상 유지하는 방법
move C,tg=p0,spd=100%,accu=1,tool=1
move C,tg=p1,spd=100%,accu=1,tool=1 // 원호 보간 수행
move P,tg=p1,spd=100%,accu=1,tool=1
stop
move C,tg=p2,spd=100%,accu=1,tool=1
move C,tg=p3,spd=100%,accu=1,tool=1 // 원호 보간 수행
end
```

