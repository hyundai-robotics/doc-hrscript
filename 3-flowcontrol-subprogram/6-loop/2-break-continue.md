# 3.6.2 break문, continue문

### 설명

이 전 절에서 설명한 `for`~`next`문 사이에서 사용합니다.

- `for`~`next` 블록 내에서 `break`문을 만나면, 반복을 중단하고 `next` 다음 명령문으로 분기합니다.
- `for`~`next` 블록 내에서 `continue`문을 만나면, 다음 명령문으로 진행하지 않고 인덱스변수의 증감을 수행한 후 `for`문으로 분기합니다.

### 문법

```python
for <인덱스변수>=<초기값> to <종료값> [step <증감값>]
	<명령문>
	…
	break
	<명령문>
	…
next
```

```python
for <인덱스변수>=<초기값> to <종료값> [step <증감값>]
	<명령문>
	…
	continue
	<명령문>
	…
next
```

### 사용 예

for~next문을 이용하여 배열의 모든 이름을 출력하되, 5자를 초과하는 이름은 제외하고, 공문자열을 만나면 중단하는 예입니다.

```python
var i
var names=["Anna", "James", "George", "Brenda", "Tom", "", "Kate"]
var n_name = len(names)
for i=0 to n_name-1
   var name=names[i]
	if name==""
	   break
	endif
   if len(name)>5
	   continue
	endif
	print name
next
end
```

실행결과

```python
Anna
James
Tom
```
