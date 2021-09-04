# put

### 설명

HTTP PUT 서비스를 요청합니다.

전송할 데이터는 body 속성에 미리 대입해 두어야 합니다.

### 문법

&lt;HttpCli객체&gt;.put &lt;URL 문자열&gt;

### 사용 예

```python
var domain="http://192.168.1.200:8888"
cli.body=500
cli.put domain+"/setting/max_torque"
```


