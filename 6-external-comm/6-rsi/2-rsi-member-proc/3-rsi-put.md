# put

### 설명

RSI의 put() 함수를 실행하여 기존 태그의 값을 변경하거나 옵션 태그를 추가할 수 있습니다.


### 문법

&lt;RSI객체&gt;.put("cmd_po") 
&lt;RSI객체&gt;.put("trigger", 1) 

### 리턴값
- 1: 기존 태그에 값을 변경
- 0: 옵션 태그를 추가


### 사용 예

```python
var ret
ret=rsi.put("cmd_po")  # "cmd_po" 태그를 추가하여 로봇의 지령위치를 전달
ret=rsi.put("trigger", 1)  # trigger 태그에 값을 1로 변경
ret=rsi.put("MyValue1", 789)  # MyValue1 태그를 추가하여 정수값 789 설정
ret=rsi.put("MyValue2", 1.2345)  # MyValue2 태그를 추가하여 실수값 1.2345 설정
ret=rsi.put("MyValue3", "hello")  # MyValue3 태그를 추가하여 문자열 "hello"를 지정
```



