# 5.4 move문

move문은 로봇을 움직이는 프로시져입니다. 형식은 아래와 같습니다.

### 설명

로봇의 툴 끝이 포즈 위치로 이동합니다.

### 문법

```python
move <보간>, [tg=<포즈/시프트>], spd=<속도>, accu=<정밀도>, tool=<툴 번호> [, x=<대입문들>] [until <조건식>]
```

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
      <td style="text-align:left">대입문들</td>
      <td style="text-align:left">
        <p>move 출발 시, 수행 할 대입문들의 문자열
          <br
          />
        </p>
        <p>왼쪽부터 세미콜론(;)으로 분할된 각 대입문들이 수행됩니다.
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

---
### 보간

스텝과 스텝 사이의 보간 된 경로를 말하며 [스텝 N]의 보간 방법은 [스텝 N-1]과 [스텝 N] 사이의 경로 형태를 결정합니다.

P - PTP (point to point)
각 조인트들이 출발 위치로부터 목표 위치까지 최단 경로로 이동합니다. 이때, 툴의 이동 경로를 별도로 고려하지는 않기 때문에 툴 이동 경로는 예측이 어렵습니다.


![](../_assets/move/PTP.png)

L - 직선보간
두 스텝 사이를 직교 공간상에서 직선으로 이동합니다. 아크 용접구간 등 직선 경로가 필요한 경우에 사용하며 다음의 그림과 같이 손목자세를 자동적으로 변화시키며 이동합니다.

![](../_assets/move/L.png)

직선 보간은 로봇의 손목자세를 자동으로 변화시키며 이동하는데 특정한 조건에서는 손목자세를 자동으로 변화시키지 못합니다. 이 조건을 Singular 자세라고 합니다.


{% hint style="info" %}
다음은 Singular 자세로서 자세 보간이 불가능합니다.
* B축이 Dead zone 근처인 경우입니다. Dead zone 설정은 『[F2]: 시스템』 → 『3: 로봇 파라미터』 → 『5: B축 비사용구역』을 참고하십시오.
* B축의 부호가 바뀌는 경우입니다. 즉, B축 각도의 부호가 『-』 → 『+』로 또는 『+』 → 『-』로 전환되는 경우입니다.
* R2, R1축 각도 변화가 180도를 초과하는 경우입니다.
* S축 회전중심을 B축 중심이나 Tool끝이 지나가는 경우입니다. 자세는 물론이고, 궤적오차나 Error가 발생할 수도 있습니다.
* S축 각도 변화가 180을 초과하는 경우입니다.
{% endhint %}

C - 원호보간

두 스텝 사이를 원호로 생성되는 경로로 이동합니다. 원을 결정하려면 3점이 필요한데 이를 선정하는 기준은 다음과 같습니다.

[스텝 n]에서 [스텝 n+1]로 이동할 때 [스텝 n+1]의 보간 방법이 원호보간 C 이면 다음스텝 [스텝 n+2]를 참조합니다. 만약 [스텝 n+2]의 보간 방법도 원호보간 C 라면 [스텝 n] [스텝 n+1] [스텝 n+2]로 원을 결정하여 그 중에서 [스텝 n]~[스텝 n+1] 구간의 호를 따라 이동합니다. [스텝 n+2]의 보간 법이 원호 보간이 아니면 이전스텝 [스텝 n-1]을 참조하여 [스텝 n-1][스텝 n][스텝 n+1]로 원을 결정하여 그 중에서 [스텝 n]~[스텝 n+1] 구간의 호를 따라 이동합니다.

![](../_assets/move/C1.png)

위에서 설명한 기준을 이용하면 연속원호의 경우도 동일점 중복스텝을 이용하여 프로그램을 작성할 수 있습니다.

이처럼 이동할 경로를 고려하여 스텝의 보간 법을 결정하고 동일점 중복스텝을 이용하면 원하는 대로 프로그램을 작성할 수 있습니다.


![](../_assets/move/C2.png)

시작점, 목표점, 참조점의 3점 중 두개 위치가 중복스텝이거나, 3 점이 일직선에 있으면 목표 위치까지 직선으로 이동 합니다.

![](../_assets/move/C3.png)