# 6.3 http\_cli 모듈 : HTTP 클라이언트

Hi6 제어기의 범용 이더넷 포트를 통해, 원격의 웹 서비스에 접근하여 HTTP 서비스를 받을 수 있습니다.

이 기능을 사용하기 위해서는 아래와 같이 http\_cli 모듈을 import한 후, HttpCli 객체를 생성해야 합니다.

```python
import http_cli
var cli=http_cli.HttpCli()
```

HttpCli 객체를 생성한 후에는 get, put, post, delete 멤버 프로시져를 호출하여 서비스 요청할 하면 됩니다.

HttpCli 객체는 body라는 이름의 속성을 가지고 있습니다.

get 서비스를 요청하여 성공적으로 응답을 받으면 원격 서버가 응답으로 보내준 데이터는 body 속성이 갖고 있게 됩니다. body 속성 값의 타입은 문자열일 수도 있고, 숫자나 배열, 객체일 수도 있습니다.

put 서비스를 요청할 때는, body 속성에 미리 전송할 데이터를 대입해두어야 합니다.

post 서비스를 요청할 때는 body 속성에 미리 전송할 데이터를 대입해두어야 하며, 원격 서버가 응답으로 보내준 데이터는 body 속성에 보관됩니다.

delete 서비스는 body 속성을 사용하지 않습니다.



