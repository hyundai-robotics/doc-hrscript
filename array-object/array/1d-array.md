# 4.1.1 배열

배열은 여러 개의 값을 하나의 이름으로 모아 저장해 놓고, 인덱스\(index\) 번호를 통해 접근하는 변수형입니다.

배열은 다른 변수처럼 var이나 global로 정의합니다. 배열의 정의와 접근 형식은 아래와 같습니다.

|  |  |
| :--- | :--- |
| 정의 | var 배열명 = \[ 값, 값, …\] |
| 접근 | 배열명\[인덱스\] |

배열을 구성하는 값들을 요소\(element\)라고 합니다. 위 배열 distances에는 총 5개의 요소가 있습니다. 인덱스는 0부터 시작합니다. distances의 0번 요소는 10, 1번 요소는 10.5 입니다.

배열의 특정 요소값을 읽거나 쓸 때는 아래와 같이 \[ \] 연산자를 사용합니다.

아래는 객체 정의하고 접근 한 예입니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var distances = [ 10, 10.5, 12.7, 11.92, 9.5 ]
          <br />
        </p>
        <p>distances[1]=20.5
          <br />
        </p>
        <p>print distances[0], distances[1]
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">
        <p>10
          <br />
        </p>
        <p>20.5</p>
        <p>
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

배열의 요소 개수는 len\( \) 함수로 얻을 수 있습니다. 앞에서 len\( \) 함수는 문자열의 길이를 얻는 함수로서 소개된 바 있습니다. 그런데, len\( \)의 매개변수로 배열을 넣으면 배열의 요소 개수를 리턴해줍니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
      <th style="text-align:left">결과</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">len(a)</td>
      <td style="text-align:left">
        <p>a가 문자열이면 문자열의
          길이를 리턴합니다.
          <br />
        </p>
        <p>a가 배열이면 배열의 요소
          개수를 리턴합니다.
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>len(&quot;HELLO&quot;)
          <br />
        </p>
        <p>len([20, 30, 80])
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>5</p>
        <p>3</p>
      </td>
    </tr>
  </tbody>
</table>

배열의 모든 요소들에 대해 어떤 처리를 수행하는 경우에는 주로 for~next 문이 사용됩니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var distances = [ 10, 10.5, 12.7, 11.92, 9.5]
          <br />
        </p>
        <p>for i=0 to len(distances)-1
          <br />
        </p>
        <p>distances[i] = distances[i]+10
          <br />
        </p>
        <p>print distances[i]
          <br />
        </p>
        <p>next
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">
        <p>20
          <br />
        </p>
        <p>20.5
          <br />
        </p>
        <p>22.7
          <br />
        </p>
        <p>21.92
          <br />
        </p>
        <p>19.5
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

배열 안에 저장되는 값들은 서로 다른 타입이어도 상관없습니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var arr = [ 10, &quot;abc&quot;, true]
          <br />
        </p>
        <p>for i=0 to 2
          <br />
        </p>
        <p>print arr[i]
          <br />
        </p>
        <p>next
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">
        <p>10
          <br />
        </p>
        <p>abc
          <br />
        </p>
        <p>true
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>



