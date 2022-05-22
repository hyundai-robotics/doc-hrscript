# 3.5. 내포된 \(nested\) 제어문

제어문의 블록 안에는 아래 형태와 같이 또 다른 제어문의 블록이 배치될 수 있습니다. 아래 형태에는 2단계의 내포를 보였지만 필요한 만큼 여러 단계의 내포도 가능합니다.

```python
if <bool 표현식>
	if <bool 표현식>
		<명령문 A>
		…
	else
		<명령문 B>
		…
	endif
endif
```

내포된 if문의 예를 아래에 보였습니다.

```python
var pressure=95, limit=90, inject_on=true
if inject_on
	if pressure > limit
		print "경고: 압력이 높습니다."
	else
		print "정상 동작 중."
	endif
endif
end
```



