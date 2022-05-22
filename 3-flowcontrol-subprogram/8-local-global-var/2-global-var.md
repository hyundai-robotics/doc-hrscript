# 3.8.2 전역변수

### 설명

global로 정의하는 전역 변수는 모든 JOB프로그램에서 항상 접근할 수 있습니다. 한번 정의되면 메인 프로그램의 end문이나 R0 \[ENTER\] 조작에 의해 프로그램 사이클이 리셋되어도 소멸되지 않습니다.

### 사용 예

global x가 처음 수행되면 변수 x가 생성되면서 default값 0으로 초기화되고, 다음 행에서 1로 증가합니다. 다음 프로그램 사이클에서 global x가 다시 수행될 때 x는 이미 정의되어 있기 때문에 새로 정의되지 않고 값 1도 보존됩니다. 반면 global y=10 은 정의와 함께 대입을 수행하며 다음 프로그램 사이클에서 수행되면 y변수값이 10으로 재초기화됩니다.

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
      <td style="text-align:left">틀린 교시</td>
      <td style="text-align:left">
        <p>global count=0
          <br />
        </p>
        <p>count=count+1
          <br />
        </p>
        <p>…
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">올바른 교시</td>
      <td style="text-align:left">
        <p>global count
          <br />
        </p>
        <p>count=count+1
          <br />
        </p>
        <p>…
          <br />
        </p>
        <p>end</p>
      </td>
    </tr>
  </tbody>
</table>

