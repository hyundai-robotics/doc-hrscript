# 4.2 객체 \(object\)

앞서, 배열은 여러 개의 요소값을 보관할 수 있고, 인덱스로 접근한다는 것을 배웠습니다.

객체는 여러 요소 값을 보관한다는 점에서는 배열과 같습니다. 다른 점은 인덱스가 아닌 키\(key\)로 접근한다는 점입니다. 키는 숫자가 아닌 문자열입니다.

객체는 다른 변수처럼 var이나 global로 정의합니다. 객체의 정의와 접근 형식은 아래와 같습니다.



|  |  |
| :--- | :--- |
| 정의 | var 객체명 = { 키 : 값, 키 : 값, …} |
| 접 | 객체명.키 |

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
        <p>var gap = { x:200, y:152.6 }
          <br />
        </p>
        <p>gap.x = gap.x + 10
          <br />
        </p>
        <p>print gap.x, gap.y
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">210 152.6</td>
    </tr>
  </tbody>
</table>

객체의 키는 반드시 식별자 형식이어야 하지만, 요소의 값은 모든 타입이 허용되며 서로 다른 타입이어도 상관없습니다.

객체는 요소로서 다른 객체나 배열을 포함할 수 있습니다. 마찬가지로 배열도 요소로서 다른 배열이나 객체를 포함할 수 있습니다. 아래 예에서, 객체 work는 객체 size와 배열 heights를 포함하고 있습니다.

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
        <p>var work = { part_no:3, name: &quot;gear&quot;, tested : false
          <br />
        </p>
        <p>, size : { x : 150, y : 80 }
          <br />
        </p>
        <p>, heights : [ 72.89, 74.91, 81.03, 87.60, 87.11 ] }
          <br />
        </p>
        <p>print work.tested, work.size.y, work.heights[3]
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>

      <td style="text-align:left">false, 80, 87.600000</td>
    </tr>
  </tbody>
</table>

