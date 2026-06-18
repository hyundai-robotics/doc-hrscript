# 6.6.1 생성자

### 설명

RSI 객체의 전역변수를 생성합니다.

### 문법

com.RSI(enet object) <br>

이더넷 통신 설정에서 사용하는 객체를 지정합니다. <br>
예를 들어 사용하는 객체의 이름이 "enet0"라면 _enet0를 지정하고, "enet1"라면 _enet1로 지정합니다.  

### 리턴값

생성된 객체의 참조

### 사용 예

```python
global rsi
rsi=com.RSI(_enet0)  # _enet0는 이더넷 통신 설정에서 "enet0"의 객체를 사용 
```



