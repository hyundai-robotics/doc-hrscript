# 3.4.3 복문 if~else~endif 문

### 설명

false일 경우 수행할 명령문들도 있는 경우에는 아래의 형태를 사용합니다.

표현식이 true이면 명령문 A들을 수행하고, false이면 명령문 B들을 수행합니다.

### 문법

```python
if <bool 표현식>
	<명령문 A>
	…
else
	<명령문 B>
	…
endif
```

### 사용 예

```python
var pressure=95, limit=90, exceed
if pressure > limit
	exceed = pressure - limit
	print "경고: 압력이 너무 높습니다."
else
	print "정상 동작 중."
endif
end
```



