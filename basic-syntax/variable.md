# 2.6 변수

변수\(variable\)란 값을 저장하는 공간이며, 식별자 이름을 가지고 있습니다. 변수는 전역변수\(global variable\)와 지역변수\(local variable\)로 나뉘는데 그 차이는 뒤에서 설명하겠습니다. 일단 여기서는 지역변수로 예를 들어 설명합니다.



변수는 아래와 같이 var 명령어로 만들 수 있으며 이를 변수를 정의\(define\)한다고 합니다. var 명령어 뒤에 여러 개의 식별자를 열거하여, 한꺼번에 만들 수도 있습니다.

```python
var myvar
var width, height, depth
```

변수에 값을 저장하는 것을 대입\(assign\)한다고 합니다. 대입은 변수를 정의하면서 할 수도 있고, 정의한 후에 할 수도 있습니다. 정의할 때 대입을 같이 하지 않으면 기본적으로 숫자 값 0을 갖게 됩니다.

```python
var myvar=0
var message, width=200
message="Invalid input value"
```

대입을 할 때 대입연산자\(=\)를 사용했습니다. HRScript에서 = 는 같다는 뜻이 아니라, 연산자 우변의 값을 좌변의 변수에 대입한다는 의미입니다. 이제 변수에 저장된 값을 print 문으로 출력해 봅시다.

```python
var myvar=0
var message, width=200
message="Invalid input value"
print width, message
```

이미 값이 대입된 변수에 다른 값을 대입할 수도 있습니다. 갖고 있는 값이 변할 수 있기 때문에 변수\(variable\)이라고 부르는 것입니다.

```python
var width=200
width=300
```



