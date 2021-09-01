# 3.8 지역변수와 전역변수

지금까지는 var문으로 정의한 지역변수의 예만으로 예제를 설명해왔습니다. 지역변수는 하나의 JOB 프로그램 내에서 var문에 의해 생성된 후, end문을 만나 프로그램이 종료되면 자동으로 소멸됩니다. 그리고 다른 프로그램에서는 값을 읽거나 쓸 수 없습니다.



아래의 예에서 main\_v는 0001.job 내에서만 접근 가능한 지역변수이고, sub\_v는 내에서만 접근 가능한 지역변수입니다. 다른 프로그램에서 접근하려고 하면 에러가 발생합니다.

지역변수 x는 0001.job과 0107.job에서 모두 정의했습니다. 이름이 같지만 서로 다른 변수이기 때문에, 서브 프로그램 0107에서 값으로 5를 설정했지만, 메인 프로그램 0001로 리턴한 후에는 5가 아닌 3이 출력됩니다. 

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
        <p>var main_v=10
          <br />
        </p>
        <p>var x=3
          <br />
        </p>
        <p>call 107
          <br />
        </p>
        <p>print main_v # ok
          <br />
        </p>
        <p>print sub_v # error
          <br />
        </p>
        <p>print x # 3&#xC774; &#xCD9C;&#xB825;&#xB428;.
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0107.job</td>
      <td style="text-align:left">
        <p>var sub_v=20
          <br />
        </p>
        <p>var x
          <br />
        </p>
        <p>print sub_v # ok
          <br />
        </p>
        <p>print main_v # error
          <br />
        </p>
        <p>x=5
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

반면 global로 정의하는 전역 변수는 모든 JOB프로그램에서 항상 접근할 수 있습니다. 한번 정의되면 메인 프로그램의 end문이나 R0 \[ENTER\] 조작에 의해 프로그램 사이클이 리셋되어도 소멸되지 않습니다.

아래 예의 global x가 처음 수행되면 변수 x가 생성되면서 default값 0으로 초기화되고, 다음 행에서 1로 증가합니다. 다음 프로그램 사이클에서 global x가 다시 수행될 때 x는 이미 정의되어 있기 때문에 새로 정의되지 않고 값 1도 보존됩니다. 반면 global y=10 은 정의와 함께 대입을 수행하며 다음 프로그램 사이클에서 수행되면 y변수값이 10으로 재초기화됩니다.

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
        <p>global x
          <br />
        </p>
        <p>x=x+1
          <br />
        </p>
        <p>call 107
          <br />
        </p>
        <p>print x, y # 4, 10
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0107.job</td>
      <td style="text-align:left">
        <p>global y=10
          <br />
        </p>
        <p>print x, y # 3, 10
          <br />
        </p>
        <p>x=x+1
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

따라서 전역변수를 프로그램 사이클 횟수를 위한 카운터로 활용하고자 할 때에는 정의와 함께 값을 대입해서는 안됩니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#xD2C0;&#xB9B0; &#xAD50;&#xC2DC;</td>
      <td style="text-align:left">
        <p>global count=0
          <br />
        </p>
        <p>count=count+1
          <br />
        </p>
        <p>&#x2026;
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#xC62C;&#xBC14;&#xB978; &#xAD50;&#xC2DC;</td>
      <td style="text-align:left">
        <p>global count
          <br />
        </p>
        <p>count=count+1
          <br />
        </p>
        <p>&#x2026;
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

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
        <p>end
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

