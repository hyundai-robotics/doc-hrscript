# 3.4.4. 복문 if~elseif~else~endif문

조건이 여러 개일 경우에는 아래와 같은 형태로 elseif문을 사용할 수 있습니다.

```python
if <bool 표현식>
	<명령문 A>
	…
elseif <bool 표현식>
	<명령문 B>
	…
elseif <bool 표현식>
	<명령문 C>
	…
else
	<명령문 N>
	…
endif
```

사용 예는 아래와 같습니다.

```python
var pressure=95, limit_h=90, limit_m=80
if pressure > limit_h
	print "경고: 압력이 매우 높습니다."
elseif pressure > limit_m
	print "알림: 압력이 높습니다.."
else
	print "정상 동작 중."
endif
end
```



