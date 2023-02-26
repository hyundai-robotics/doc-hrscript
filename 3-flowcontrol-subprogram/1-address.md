# 3.1 주소 \(Address\)

순서대로 다음 행을 수행하지 않고 프로그램의 다른 위치로 이동하는 것을 분기\(branch\)라고 합니다. 주소란 분기의 목적지\(destination\) 입니다.주소를 정의하는 방법은 아래와 같이 3가지 형식이 있습니다.



<table>
  <thead>
    <tr>
      <th style="text-align:left">종류</th>
      <th style="text-align:left">형식</th>
      <th style="text-align:left">예</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">행번호 (line-number)</td>
      <td style="text-align:left">
        1~9999 의 정수입니다. 스텝(move)이 아닌 명령문의 왼쪽에 지정할 수 있습니다.
      </td>
      <td style="text-align:left">99</td>
    </tr>
    <tr>
      <td style="text-align:left">레이블 (label)</td>
      <td style="text-align:left">
        레이블은 명령문에 지정하는 것이 아니라 그 자체로 명령문입니다.<br>
        \* 뒤에 [식별자](2-identifier.md)를 붙인 형식입니다. 단 식별자의 길이는 128자 이하여야 합니다.
      </td>
      <td style="text-align:left">*timeout</td>
    </tr>
    <tr>
      <td style="text-align:left">스텝 번호 (step number)</td>
      <td style="text-align:left">
        스텝(move) 명령문에 자동으로 1씩 증가하며 매겨집니다.<br>
        S뒤에 스텝의 번호를 붙인 형식입니다. S1~S999까지 지정 가능합니다.
      </td>
      <td style="text-align:left">S15</td>
    </tr>
  </tbody>
</table>


아래의 예에서 두 번째 명령문의 10은 행번호이고, \*err_handle은 레이블, S12는 스텝 번호입니다.

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
  10 z_pos = (base_height+offset)*1.05
     # robot has to wait sensor2 input
     *err_handle
S12  move P,spd=80%,accu=1,tool=3
```
