# 5.6 selucrd문

selucrd문은 조건설정의 사용자 좌표계로 지정되어 있는 사용자 좌표계 번호를 변경하기 위한 프로시져입니다.

### 설명

조건설정의 사용자(User) 좌표계 지정에 해당하는 기능입니다.


### 문법

```python
selucrd <좌표계번호>
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
      <td style="text-align:left">좌표계 번호</td>
      <td style="text-align:left">
        선택할 사용자 좌표계 번호<br>
        <ul>
        <li>0: 사용자 좌표계 지정 해제</li>
        <li>1~20: 사용자 좌표계 지정</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
   selucrd 1
   end
```