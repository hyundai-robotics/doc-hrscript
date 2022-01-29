# 2.9.1 수학 함수

<table>
  <thead>
    <tr>
      <th style="text-align:left">함수</th>
      <th style="text-align:left">설명</th>
      <th style="text-align:left">사용 예</th>
      <th style="text-align:left">결과</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">abs(a)</td>
      <td style="text-align:left">a의 절대값 (absolute) 을 리턴합니다.</td>
      <td
      style="text-align:left">abs(-300)</td>
        <td style="text-align:left">300</td>
    </tr>
    <tr>
      <td style="text-align:left">acos(a)</td>
      <td style="text-align:left">a의 arc cosine값을 radian 형식으로
        리턴합니다.</td>
      <td style="text-align:left">acos(0.5)</td>
      <td style="text-align:left">1.0472</td>
    </tr>
    <tr>
      <td style="text-align:left">asin(a)</td>
      <td style="text-align:left">a의 arc sige 값을 radian 형식으로
        리턴합니다.</td>
      <td style="text-align:left">asin(0.5)</td>
      <td style="text-align:left">0.5236</td>
    </tr>
    <tr>
      <td style="text-align:left">atan(a)</td>
      <td style="text-align:left">a의 arctangent 값을 radian 형식으로
        리턴합니다.</td>
      <td style="text-align:left">atan(0.5)</td>
      <td style="text-align:left">0.4636</td>
    </tr>
    <tr>
      <td style="text-align:left">atan2(a, b)</td>
      <td style="text-align:left">y길이가 a, x길이가 b인 삼각형의
        arctangent 값을 radian 형식으로 리턴합니다.</td>
      <td
      style="text-align:left">atan2(2,1)</td>
        <td style="text-align:left">1.1071</td>
    </tr>
    <tr>
      <td style="text-align:left">cos(r)</td>
      <td style="text-align:left">radian 형식의 a의 cosine 값을 리턴합니다.</td>
      <td
      style="text-align:left">cos(3.1415)</td>
        <td style="text-align:left">-1</td>
    </tr>
    <tr>
      <td style="text-align:left">deg2rad(d)</td>
      <td style="text-align:left">degree 형식의 d의 radian 값을 리턴합니다.</td>
      <td
      style="text-align:left">deg2rad(-90)</td>
        <td style="text-align:left">-1.570796</td>
    </tr>
    <tr>
      <td style="text-align:left">dist(x, y)</td>
      <td style="text-align:left">원점에서 (x, y) 좌표까지의
        유클리드 거리를 리턴합니다.</td>
      <td
      style="text-align:left">dist(3.5,10)</td>
        <td style="text-align:left">10.59481</td>
    </tr>
    <tr>
      <td style="text-align:left">max(a, b)</td>
      <td style="text-align:left">a와 b중 큰 값을 리턴합니다.</td>
      <td
      style="text-align:left">max(-1.23, -3)</td>
        <td style="text-align:left">-1.23</td>
    </tr>
    <tr>
      <td style="text-align:left">min(a, b)</td>
      <td style="text-align:left">a와 b중 작은 값을 리턴합니다.</td>
      <td
      style="text-align:left">max(-1.23, -3)</td>
        <td style="text-align:left">-3</td>
    </tr>
    <tr>
      <td style="text-align:left">near(a, b[,e])</td>
      <td style="text-align:left">실수값 a와 b의 차이가
        e보다 작거나 같으면 1,
        크면 0을 리턴합니다.</td>
      <td
      style="text-align:left">
        <p>near(0.005, 0.0058)
          <br />
        </p>
        <p>near(0.005, 0.006)
          <br />
        </p>
        <p>near(0.005, 0.006, 0.1)
          <br />
        </p>
        </td>
        <td style="text-align:left">
          <p>1</p>
          <p>0</p>
          <p>1</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">rad2deg(r)</td>
      <td style="text-align:left">radian 형식의 r의 degree값을 리턴합니다.</td>
      <td
      style="text-align:left">rad2deg(1.570796)</td>
        <td style="text-align:left">90</td>
    </tr>
    <tr>
      <td style="text-align:left">sin(r)</td>
      <td style="text-align:left">radian 형식의 r의 sine 값을 리턴합니다.</td>
      <td
      style="text-align:left">sin(1.5*3.1415)</td>
        <td style="text-align:left">-1</td>
    </tr>
    <tr>
      <td style="text-align:left">sqr(a)</td>
      <td style="text-align:left">a의 제곱근(square root)을 리턴합니다.</td>
      <td
      style="text-align:left">
        <p>sqr(16)
          <br />
        </p>
        <p>sqr(0)
          <br />
        </p>
        </td>
        <td style="text-align:left">
          <p>4
            <br />
          </p>
          <p>0
            <br />
          </p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">tan(r)</td>
      <td style="text-align:left">radian 형식의 r의 tangent 값을 리턴합니다.</td>
      <td
      style="text-align:left">tan(3.141592/4)</td>
        <td style="text-align:left">0.9999</td>
    </tr>
  </tbody>
</table>



