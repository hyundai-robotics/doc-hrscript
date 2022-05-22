# 3.4.2 복문 if~endif 문

### 설명

단문 if는 참일 경우 특정 주소로 분기하는 동작 밖에는 못합니다. 그 외의 동작, 혹은 여러 개의 명령문을 수행해야 한다면 복문 if문을 사용해야 합니다. 

형태는 다음과 같습니다. &lt;bool 표현식&gt;이 true이면 if ~ endif 사이의 &lt;명령문&gt;들을 순서대로 수행합니다. false이면 &lt;명령문&gt;들을 수행하지 않고 endif 다음 위치로 건너뜁니다.

### 문법

```python
if <bool 표현식>
	<명령문>
	…
endif
```

### 사용 예

 pressure가 limit보다 크면, 그 아래의 대입문과 print 문을 수행하지만, 그렇지 않으면 수행하지 않고 end로 분기합니다. 

```python
var pressure=95, limit=90, exceed
if pressure > limit
	exceed = pressure - limit
	print "경고: 압력이 너무 높습니다."
endif
end
```

예제 프로그램을 보면 if와 endif 사이의 명령문들이 2칸 정도 들여쓰기 되어 있습니다. 이 명령문들이 if~ endif 사이에 내포된\(nested\) 한 블록\(block\)의 코드임을 쉽게 알아볼 수 있도록 들여쓰기를 한 것입니다.

