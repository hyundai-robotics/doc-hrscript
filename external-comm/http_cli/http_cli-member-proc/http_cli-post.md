# post

### 설명

HTTP POST 서비스를 요청합니다.

전송할 데이터는 body 속성에 미리 대입해 두어야 합니다.

응답 데이터는 body 속성으로 받습니다.

### 문법

&lt;HttpCli객체&gt;.post &lt;URL 문자열&gt;

### 사용 예

```python
var domain="http://192.168.1.200:8888"
cli.body={ name: "WORK #32", color: "green", state: "OK" }
cli.post domain+"/display/update"
```

