# 6.5 sci 모듈 : 시리얼 통신

Hi6 제어기의 COM 포트를 통해, 시리얼 통신을 수행할 수 있습니다.

이 기능을 사용하기 위해서는 아래와 같이 sci 모듈을 import한 후, Sci 객체를 생성해야 합니다.

또한 사용하기 전에 반드시 [시스템 > 2. 제어파라미터 > 3. 시리얼 포트] 의 설정 사양을 확인하세요.

```python
import sci
var sci2=sci.Sci(2)
```

Sci 객체를 생성한 후에는 send, recv, open, close 멤버 프로시져를 호출하면 됩니다.

send를 호출할 때는, 미리 전송할 문자열을 대입해두어야합니다.

recv를 호출할 때는, 성공적으로 수신하면 응답 문자열을 반환합니다. 

open를 호출하여 port를 open 하게 됩니다. 

close를 호출하여 port를 close 하게 됩니다.



