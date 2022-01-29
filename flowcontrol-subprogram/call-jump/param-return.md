# 3.7.2 매개변수와 param문, return문

JOB 프로그램은 입력과 출력을 전달하는 통로\(channel\)로서 형식 매개변수를 사용합니다. 형식 매개변수는 JOB 프로그램의 가장 선두에 param 명령문으로 정의합니다.

아래 예에서 105번 JOB은 원점으로부터 좌표값\(x,y\)까지의 유클리드 거리를 구하여 len으로 리턴하는 서브 JOB으로서 dist2d라고 이름을 지었습니다.

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
        <p>var x,y
          <br />
        </p>
        <p>x=5
          <br />
        </p>
        <p>y=12.8
          <br />
        </p>
        <p>call 105_dist2d,x,y
          <br />
        </p>
        <p>var res=result()
          <br />
        </p>
        <p>print res
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0105_dist2d.job</td>
      <td style="text-align:left">
        <p># Calc. Euclide distance 2D
          <br />
        </p>
        <p>param x,y
          <br />
        </p>
        <p>var tmp
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>tmp=x*x+y*y
          <br />
        </p>
        <p>var len=sqr(tmp) # distance from origin
          <br />
        </p>
        <p>return len
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">13.742</td>
    </tr>
  </tbody>
</table>

1번 JOB에서 이 dist2d 서브 프로그램을 call 문으로 호출하고 있으며, 지역변수인 x, y를 전달하고 있습니다. dist2d  서브 프로그램 내에서 param문으로 정의한 ldX, ldY를 형식 매개변수\(formal parameter\)라고 하며, call 문에 전달한 x, y를 실 매개변수\(actual parameter\)라고 합니다.

dist2d 프로그램은 결과값을 return 문을 통해 외부로 전달하고 있습니다. 이 return값은 호출한 프로그램에서 result\(\) 함수를 호출하여 얻을 수 있습니다.

\(return문과 end문은 프로그램을 종료하고 주 프로그램으로 리턴한다는 점에서 동작이 같습니다. 다만 return문은 결과값을 인수로 지정할 수 있다는 점에서만 end문과 다릅니다.\)



