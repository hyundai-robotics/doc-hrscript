# 2.9.2 문자열 함수

var str="hello, world"가 실행된 상태에서의 예

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
      <td style="text-align:left">bin(a)</td>
      <td style="text-align:left">수치 a의 2진 표현 문자열을 리턴합니다</td>
      <td style="text-align:left">bin(0b0010)</td>
      <td style="text-align:left">&quot;10&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">chr(a)</td>
      <td style="text-align:left">ASCII코드 a인 문자를 문자열형으로 리턴합니다.</td>
      <td style="text-align:left">chr(65)</td>
      <td style="text-align:left">&quot;A&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">double(s)</td>
      <td style="text-align:left">
        <p>실수 문자열s의 실수형값을 리턴합니다.
          <br />
        </p>
        <p>(해석되는 위치까지만 해석하고 나머지는 버림)
          <br
          />
        </p>
      </td>
      <td style="text-align:left">double(&quot;29.38E-2&quot;)</td>
      <td style="text-align:left">0.2938</td>
    </tr>
    <tr>
      <td style="text-align:left">hex(a)</td>
      <td style="text-align:left">수치 a의 16진 표현 문자열을 리턴 합니다.</td>
      <td style="text-align:left">hex(0x7A2F)</td>
      <td style="text-align:left">&quot;7A2F&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">int(s)</td>
      <td style="text-align:left">
        <p>정수 문자열s의 정수형값을 리턴합니다.
          <br />
        </p>
        <p>(해석되는 위치까지만 해석하고 나머지는 버림)
          <br
          />
        </p>
      </td>
      <td style="text-align:left">
        <p>int(&quot;13.25&quot;)
          <br />
        </p>
        <p>int(&quot;29.38E-2&quot;)
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>13
          <br />
        </p>
        <p>29
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">left(s, n)</td>
      <td style="text-align:left">문자열 s의 앞부분 n개의 문자로 된 문자열을 리턴합니다.</td>
      <td
      style="text-align:left">left(str, 3)</td>
        <td style="text-align:left">&quot;hel&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">len(s)</td>
      <td style="text-align:left">
        <p>s가 문자열이면 문자열의 길이를 리턴합니다.
          <br />
        </p>
        <p>s가 배열이면 배열의 요소 개수를 리턴합니다.
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
        <p>5
          <br />
        </p>
        <p>3
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">mid(s, i, n)</td>
      <td style="text-align:left">문자열 s의 i번째 문자부터 n개의 문자로 된 문자열을 리턴합니다. (첫 문자 위치는 0.)</td>
      <td style="text-align:left">mid(str, 3, 5)</td>
      <td style="text-align:left">&quot;lo, w&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">mirror(s)</td>
      <td style="text-align:left">문자열 s를 역전한 문자열을 리턴합니다.</td>
      <td style="text-align:left">mirror(&quot;HELLO&quot;)</td>
      <td style="text-align:left">&quot;OLLEH&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">right(s, n)</td>
      <td style="text-align:left">문자열 s의 뒷부분 n개의 문자로 된 문자열을 리턴합니다.</td>
      <td
      style="text-align:left">right(str, 3)</td>
        <td style="text-align:left">&quot;rld&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">str(a)</td>
      <td style="text-align:left">수치 a의 10진 표현 문자열을 리턴합니다.</td>
      <td style="text-align:left">str(13.25)</td>
      <td style="text-align:left">13.250000</td>
    </tr>
    <tr>
      <td style="text-align:left">strpos(s, p)</td>
      <td style="text-align:left">s문자열 내에 p문자열과 일치하는 최초의 위치를 리턴합니다.(첫 문자 위치는 0. 없으면 -1.)</td>
      <td style="text-align:left">
        <p>strpos(str, &quot;llo&quot;)
          <br />
        </p>
        <p>strpos(str, &quot;hi&quot;)
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>2
          <br />
        </p>
        <p>-1
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>



