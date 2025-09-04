# _pc 문

### 설명

_Pc문은 현재 프로그램 카운터 정보를 얻기 위해서 사용합니다. <br>
프로그램 카운터는 프로그램 번호, 스텝 번호, 펑션 번호로 구성되어 있습니다.

### 문법

```python
var sno=_pc.cur_sno  # 현재 스텝번호를 대입
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">cur_sno</td>
      <td style="text-align:left">
         현재 커서가 위치한 곳의 스텝 번호
      </td>
      <td style="text-align:left">변수</td>
    </tr>
  </tbody>
</table>




### cur_sno 사용 예 : until 조건 불만족시 이전 스텝으로 이동 

```python
   S6 move P,spd=50%,accu=3,tool=1,until di6
      if (result()==0)
        goto S[_pc.cur_sno-1]
      endif
   S7 move P,spd=50%,accu=3,tool=1,until di7
      if (result()==0)
        goto S[_pc.cur_sno-1]
      endif
   S8 move P,spd=50%,accu=3,tool=1,until di8
      if (result()==0)
        goto S[_pc.cur_sno-1]
      endif
   ...
```

