# 3.8.3 우선순위

동일한 이름을 가진 지역변수와 전역변수가 있을 때에는 지역변수에 우선적으로 접근합니다. 가령, 아래 0005.job이 수행되는 동안은 전역변수 x와 지역변수 x가 동시에 존재하게 되는데, 이 때 x값을 읽어보면 지역변수가 읽힙니다. 0005.job에서 0001.job으로 리턴한 후, x값을 읽어보면 전역변수만 존재하는 상태이므로 전역변수가 읽힙니다.

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
        <p>global x=100
          <br />
        </p>
        <p>call 5
          <br />
        </p>
        <p>print x # 100
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0005.job</td>
      <td style="text-align:left">
        <p>var x=&quot;hello&quot;
          <br />
        </p>
        <p>print x # hello
          <br />
        </p>
        <p>end</p>
      </td>
    </tr>
  </tbody>
</table>

