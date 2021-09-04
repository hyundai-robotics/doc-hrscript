# get

### 설명

HTTP GET 서비스를 요청합니다.

응답 데이터는 body 속성으로 받습니다.

### 문법

&lt;HttpCli객체&gt;.get &lt;URL 문자열&gt;

### 사용 예

```python
var domain="http://192.168.1.200:8888"
cli.get domain+"/setting/max_torque"
```



