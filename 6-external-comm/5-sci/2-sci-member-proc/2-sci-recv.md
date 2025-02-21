# recv

### 설명

Sci의 recv 를 호출하여 문자열을 수신합니다.


### 문법

&lt;Sci객체&gt;.recv 문자열 변수 \[,{대기시간}\] \[,{퇴피주소}\]


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
      <td>문자열 변수</td>
      <td>
        성공적으로 수신했을 때, 입력된 문자열을 보관할 문자열 변수<br>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>대기시간</td>
      <td>
        timeout 시간. 지정된 시간동안 데이터 수신이 없을 때 퇴피 주소로 분기하고 퇴피 주소가 없으면 에러가 발생한다.<br>
        지정하지 않으면 무한 대기한다.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        timeout 일 때 분기할 주소.<br>
        지정하지 않으면 에러로 정지한다.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>


### 사용 예

```python
   var msg
   sci2.recv msg,5000,*timeout
   print msg
   ...
   ...
   *timeout
   print "timeout error"
   stop
```



