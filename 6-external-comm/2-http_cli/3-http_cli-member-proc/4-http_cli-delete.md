# delete

### 설명

HTTP DELETE 서비스를 요청합니다.

body 속성은 사용되지 않습니다.

### 문법

&lt;HttpCli객체&gt;.delete &lt;URL 문자열&gt;

### 사용 예

```python
var domain="http://192.168.1.200:8888"
cli.delete domain+"/items/3"
```

