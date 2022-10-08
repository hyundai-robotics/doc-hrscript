# 8. 앨리어스(alias)

앨리어스\(alias\)란 변수나 객체의 속성의 표기를 대체할 수 있는 이름입니다. 반복해 사용하기에 너무 긴 속성 표기를 간결한 이름으로 대체하거나, 특정한 인덱스의 IO 변수를 가독성이 좋은 이름으로 대체해 사용할 수 있습니다.
22
앨리어스는 alias 명령문으로 정의하며, 문법은 var이나 global과 거의 같습니다.
앨리어스의 scope는 global과 동일합니다. 즉, alias 문이 실행된 후에는 이후 수행되는 어느 job에서나 사용할 수 있으며, 메인 프로그램의 end문이나 R0 \[ENTER\] 조작에 의해 프로그램 사이클이 리셋되어도 소멸되지 않습니다.

```python
global myval=3, yourname="Jane"
val i=0,msg="hello"
val profile = { name: "Paul", age: 43, role: [ "CTO", "engineer" ] }

alias grip=fb3.do4, work_no=fb1.diw2 # (1)
alias role=profile.role # (2)
alias tool0=project.robot.tools.t_0 # (3)

# 활용
grip=1
print work_no
print role[1]
tool0.mass=12
```

위 예제의 (1)에서 fb3.do4 출력변수를 grip이라는 앨리어스로 정의했고, fb1.diw2라는 입력변수를 work_no라는 앨리어스로 정의했습니다.  
(2)에서는 profile의 속성인 role 배열을 role이란 앨리어스로 정의했습니다.  
(3)에서는 내장 객체인 project.robot.tools.t_0를 tool0라는 앨리어스로 정의했는데, 이것은 0번 툴 데이터를 가리키게 됩니다.

배열을 가리키는 앨리어스는 role[1]과 같이 [] 연산자로 인덱스를 지정할 수 있습니다.  
객체를 가리키는 앨리어스는 tool0.mass와 같이 . 연산자로 속성을 지정할 수 있습니다.

상수는 alias로 정의할 수 없습니다. global이나 var을 사용해 정의하십시오.  
수식도 alias로 정의할 수 없습니다. 오동작이 발생할 수 있으므로 주의하십시오.

```python
#alias pie=3.141592 # (X)
#alias unit="mm/s" # (X)
global pie=3.141592 # (O)
global unit="mm/s" # (O)

#alias pie_2 = pie*pie # (X)
```
