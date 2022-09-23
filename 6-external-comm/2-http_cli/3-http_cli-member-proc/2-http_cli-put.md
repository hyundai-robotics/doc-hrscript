# put

### 설명

HTTP PUT 서비스를 요청합니다.

요철된 자원을 수정(update)합니다. 

전송할 데이터는 body 속성에 미리 대입해 두어야 합니다.

### 문법

&lt;HttpCli객체&gt;.put &lt;URL 문자열, 대기시간, 퇴피주소&gt;


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
cli.body=500
cli.put domain+"/setting/max_torque"

#case 2
var url = domain + "/setting"
cli.body = {max_torque: 500}
cli.put (url, 5000, S1)
```



