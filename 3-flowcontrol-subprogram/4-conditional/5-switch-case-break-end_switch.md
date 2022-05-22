# 3.4.5. switch~case~break~end\_switch문

### 설명

switch 문은 수식을 평가하여 case문으로 지정한 수식을 평가한 값과 비교합니다. 값이 일치하는 case문부터 break 문을 만날 때까지 수행합니다. 

예를 들어, 아래에서 표현식 X의 결과값이 표현식 B1이나 B2의 결과값와 같다면, \(1\) ~ \(3\)이 수행한 후 end\_switch 문 지점으로 이동합니다. \(명령문 B 밑에 break가 없는 점을 유의하십시오.\) X의 값이 C와 같을 때는 \(2\) ~ \(3\)이 수행됩니다. 

만일, X의 값이 어떤 case 문의 값과도 일치하지 않으면, default로 이동하여 \(4\) ~ \(5\)가 수행됩니다. default 구간은 없어도 됩니다.

### 문법

```python
switch <표현식X>
case <표현식A>
	<명령문 A>
	…
	break
case <표현식B1>
case <표현식B2>
	<명령문 B>	… (1)
case <표현식C>
	<명령문 C>	… (2)
	…
	break		… (3)
default
	<명령문 N>	… (4)
	…
	break		… (5)
end_switch
```

표현식은 결과가 bool, 숫자, 문자열인 상수, 변수, 수식이 모두 가능합니다.

### 사용 예

```python
     var state="timeout"
     var res=0
     
     switch state
     case "ok"
       res=11
       break
     case "timeout"
     case "timeover"
       res=33
       break
     case "invalid"
       res=55
       break
     case "fault"
       res=77
       break
     default
       res=99
       break
     end_switch
     
  99 end
```

