# 4.4 참조 전달\(call-by-reference\)와 값 전달\(call-by-value\)

3.4절의 call문과 jump문 설명에서 형식 매개변수와 실 매개변수의 개념을 배운 바 있습니다. 실 매개변수를 서브 프로그램으로 전달했는데, 서브 프로그램이 이 변수의 값을 변경한 후 종료했다면 변경된 내용이 메인 프로그램에 반영되어 있을까요?

가령, 아래와 같이 세제곱을 해주는 서브 프로그램 0005\_pow3.job를 만들었다고 합시다.

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
        <p>var x=2
          <br />
        </p>
        <p>call 0005_pow3,x
          <br />
        </p>
        <p>print x
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0005_pow3.job</td>
      <td style="text-align:left">
        <p>param p
          <br />
        </p>
        <p>var t=p
          <br />
        </p>
        <p>p=t*t*t # (1)
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">2</td>
    </tr>
  </tbody>
</table>

2\*2\*2는 8이므로 8이 출력되기를 기대했지만, 결과는 2입니다. 숫자형 실 매개변수가 서브 프로그램으로 전달될 때는 매개변수로 값\(value\)이 복사되기 때문입니다. \(1\)에서 세제곱 값을 복사본에 대입한 것이므로 원본 변수 x의 값에는 영향을 주지 못한 것입니다.

따라서, 아래와 같이 return문으로 결과값을 전달받도록 교시 프로그램을 고쳐야 합니다.

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
        <p>var x=2
          <br />
        </p>
        <p>call 0005_pow3,x
          <br />
        </p>
        <p>x=result()
          <br />
        </p>
        <p>print x
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0005_pow3.job</td>
      <td style="text-align:left">
        <p>param p
          <br />
        </p>
        <p>var t=p
          <br />
        </p>
        <p>p=t*t*t
          <br />
        </p>
        <p>return p
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">8</td>
    </tr>
  </tbody>
</table>

반면, 배열이나 객체의 경우에는 복사본이 아니라 실제 변수의 참조\(reference\)가 전달됩니다. 참조란 변수의 위치와 같은 개념입니다.



아래와 같이 배열의 각 요소를 세제곱 해주는 서브 프로그램 0006\_pow3.job의 경우에는 의도한 대로 실 매개변수 배열의 요소 값들이 변경되었습니다.

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
        <p>var x=[3, 2, 4]
          <br />
        </p>
        <p>call 0006_pow3,x
          <br />
        </p>
        <p>print x
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0006_pow3.job</td>
      <td style="text-align:left">
        <p>param p
          <br />
        </p>
        <p>var t
          <br />
        </p>
        <p>for i=0 to len(arr)-1
          <br />
        </p>
        <p>t=p[i]
          <br />
        </p>
        <p>p[i] = t*t*t
          <br />
        </p>
        <p>next
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">[27, 8, 64]</td>
    </tr>
  </tbody>
</table>

서브 프로그램 호출 시, 실 매개변수의 값의 복사본이 전달되는 것을 값에 의한 호출\(call-by-value\), 참조가 전달되는 것을 참조에 의한 호출\(call-by-reference\) 이라고 합니다. 값 호출일 지 참조 호출일 지는 아래와 같이 값의 형\(type\)에 의해 결정됩니다.

|  |  |
| :--- | :--- |
| 값에 의한 호출 | bool형, 숫자형, 문자열형 |
| 참조에 의한 호출 | 배열형, 객체형 |

![](../.gitbook/assets/image%20%283%29%20%281%29.png)



