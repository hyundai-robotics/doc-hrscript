# 3.4.1 단문 if문

### 설명

단문 if문의 형태는 다음과 같습니다. &lt;bool 표현식&gt;이 true이면 &lt;주소&gt;로 분기하고, false이면 분기하지 않고 다음 명령문으로 넘어갑니다.

### 문법

```python
if <bool 표현식> then <주소>
```

### 사용 예

pressure 가 limit보다 크다는 조건이 true인 경우, 레이블 주소인 \*err로 분기해서 압력이 너무 높다는 경고를 print합니다. false이면, 분기하지 않고 다음 명령문을 차례로 수행하기 때문에, ' 정상 동작 중.'을 출력하고 프로그램을 끝냅니다.

```python
var pressure=95, limit=90
if pressure > limit then *err
print "정상 동작 중."
end
*err
print "경고: 압력이 너무 높습니다."
```

