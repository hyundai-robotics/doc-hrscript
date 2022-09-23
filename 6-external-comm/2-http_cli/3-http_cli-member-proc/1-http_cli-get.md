# get

### 설명

HTTP GET 서비스를 요청합니다.

서버는 요청받은 URL의 정보를 검색하여 응답합니다.

응답 데이터는 body 속성으로 받습니다.

### 문법

&lt;HttpCli객체&gt;.get &lt;URL 문자열, 대기시간, 퇴피주소&gt;


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
      <td>URL 문자열</td>
      <td>
        요청 URL
      </td>
      <td></td>
    </tr>
    <tr>
      <td>대기시간</td>
      <td>
        (Optional) timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행한다.<br>
        지정하지 않으면 무한 대기한다.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        (Optional) timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행한다.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>


### 사용 예

```python
#case 1
var domain="http://192.168.1.200:8888"
cli.get domain+"/setting/max_torque"

#case 2
var url = domain+"/joints/max_speed"
cli.query = {axis: 3}
cli.get(url)
```



