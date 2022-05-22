# 4.1.2 다차원 배열

배열의 요소로서 배열이 내포될 수도 있습니다.

다차원 배열의 요소에 접근할 때는 \[ \] 연산자를 연속적으로 사용하면 됩니다.

아래의 예에서 arr\_y는 2차원 배열입니다. \(1\)

arr\_y\[1\]는 이 중 인덱스 1의 요소, 즉 \["abc", "jqk", "xyz"\] 배열인데, 이를 새로운 변수 arr\_x에 대입했습니다. \(2\)

따라서, arr\_x\[1\]은 "jqk"이고, arr\_y\[1\]\[2\]는 arr\_y\[1\]의 \[2\]를 가리키므로 "xyz"입니다.

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
        <p>var arr_y = [ [10,20], [&quot;abc&quot;,&quot;jqk&quot;, &quot;xyz&quot;]
          ] # (1)
          <br />
        </p>
        <p>var arr_x=arr_y[1] # (2)
          <br />
        </p>
        <p>print arr_x[1]
          <br />
        </p>
        <p>print arr_y[1][2]
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">
        <p>jqk
          <br />
        </p>
        <p>xyz
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

