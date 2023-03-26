# Hi6 로봇제어기 기능설명서 - 로봇언어 HRScript

{% hint style="warning" %}
본 제품 설명서에서 제공되는 정보는 현대로보틱스의 자산입니다.

현대로보틱스의 서면에 의한 동의 없이 전부 또는 일부를 무단 전재 및 재배포할 수 없으며, 제3자에게 제공되거나 다른 목적에 사용할 수 없습니다.



본 설명서는 사전 예고 없이 변경될 수 있습니다. 시험3



**Copyright ⓒ 2020 by Hyundai Robotics**
{% endhint %}
# 1. 개요


  


# 1.1 HRScript의 소개

현대로봇 hi6 제어기는 HRScript라는 이름의 로봇언어로 로봇이 할 일을 프로그램할 수 있습니다. 작성된 프로그램은 확장자 .job 을 가진 여러 개의 파일에 나뉘어 저장될 수 있습니다. HRScript는 이름에서 알 수 있듯이 스크립트 언어로서, 컴파일 절차없이 인터프리터에 의해 한 행씩 해석, 실행됩니다. python이나 javascript 언어와 유사하지만 문법은 더 간단합니다.

# 2. 기본 문법

먼저, hrscript의 기본 용어들을 설명합니다. 변수를 정의하는 방법, 그리고 연산자를 사용해 간단한 수식을 구성하고 그 결과값을 변수에 대입하는 방법을 따라가면서, job 프로그램의 기본적인 개념을 이해해 보도록 하겠습니다.

# 2.1 명령문

명령문\(statement\)이란 JOB 프로그램의 실행 단위가 되는 각각의 명령 문자열을 말합니다. hrscript는 한 행에 1개의 명령문만을 허용합니다. 아래에 4개의 명령문의 예를 보였습니다. 내용을 이해할 필요는 없습니다. 대략적인 형태만 눈여겨보세요.

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
10   z_pos = (base_height+offset)*1.05
     # robot has to wait sensor2 input
     *err_handle
```

로봇을 이동시키는 스텝 명령문\(move문 등\) 이외의 명령문에 대해서는 선택적으로 행의 선두에 행 번호\(1~9999\)를 붙일 수 있습니다. 두 번째 행에 있는 10이 행번호의 예입니다. 

명령문의 앞과 뒤에는 임의 개수의 공백이나 tab이 있어도 상관없습니다.

가독성을 위해 명령문의 적절한 들여쓰기\(indentation\)가 권장됩니다. 들여쓰기는 공백과 tab이 모두 허용되며 실행 시 동작에 영향을 주지 않습니다.



# 2.2 식별자

앞으로 설명될 명령어, 변수, 함수, 레이블은 모두 이름을 가지고 있습니다. 이 이름들을 식별자\(identifier\)라고 통칭합니다. 식별자를 정할 때는 다음과 같은 hrscript의 식별자 규칙을 따라야만 합니다.

* 영문 대소문자과 숫자, 밑줄\(underscore\)로만 구성됩니다.
* 첫 글자로는 숫자가 허용되지 않습니다. 반드시 대소문자, 혹은 밑줄이어야 합니다.
* 
  공백이나 tab을 포함할 수 없습니다.

* 
  if, for 등 시스템에서 이미 정의한 식별자는 사용할 수 없습니다.

* 
  길이는 제약이 없습니다.

다음은 식별자의 올바른 예와 잘못된 예입니다.

```text
myvar (O) 
myvar2 (O)
_myvar (O)
MyVar (0)
310a (X) ; 숫자로 시작.
move (X) ; 시스템에 이미 정의된 식별자
v300$ ; 밑줄 이외의 기호($) 사용
my var (X) ; 공백 포함
```



# 2.3 명령문의 종류

hrscript의 명령문에는 아래와 같이 4종류가 있습니다.



* 프로시져 \(procedure\)
* 대입문 \(assignment\)
* 주석문 \(comment\)
* 레이블 \(label\)



# 2.3.1 프로시져

프로시져는 명령어와 0~N개의 매개변수\(parameter\)들로 구성됩니다.

```python
move P,po3,spd=80%,accu=1,tool=3 until do33
```

프로시져 매개변수는 아래와 같이 3가지 종류가 있습니다.

| 종류 | 문법 | 예제 |
| :--- | :--- | :--- |
| 위치\(position\) 매개변수 | &lt;value&gt; | P, po3 |
| 키워드\(keyword\) 매개변수 | &lt;keyword&gt;=&lt;value&gt; | spd=80%, accu=1, tool=3 |
| 전치사\(preposition\) 매개변수 | &lt;preposition&gt; &lt;value&gt; | until do33 |

위치매개변수는 몇 번째에 위치하는지에 따라 그 역할이 결정되므로, 위치가 바뀌어서는 안 되며, 프로시져의 가장 앞 부분에 있어야 합니다. 키워드 매개변수는 위치매개변수 다음에 있어야 하지만, 키워드 매개변수들 간의 순서는 동작에 영향을 주지 않습니다.

전치사 매개변수는 맨 마지막에 배치됩니다.



# 2.3.2 대입문

대입문은 좌변과 대입 연산자\(=\), 우변으로 구성됩니다. 좌변\(lvalue\)는 반드시 값을 저장할 수 있는 변수여야 합니다. 상수나 수식은 허용되지 않습니다.

우변\(rvalue\)은 상수, 변수, 수식이 모두 허용됩니다.

```python
height=(500+margin)/2
```

# 2.3.3 주석문

job 프로그램의 내용을 이해하기 쉽도록 설명하는데 사용합니다. 주석문은 실행 되더라도 아무 동작도 수행되지 않습니다. 아래와 같이 해시 기호\(\#\) 뒤에 설명을 붙이는 형식입니다. 하나의 명령문으로서 사용할 수도 있고 다른 명령문 뒤에 붙일 수도 있습니다.

```python
# robot has to wait sensor2 input
var work_w,work_h  # 작업물의 너비와 높이
```



# 2.3.4 레이블

goto 문에 의해 이동할 목표 지점을 표시합니다. 별표\(\*\)와 식별자로 구성됩니다.

# 2.4 첫 번째 프로그램 - Hello, World !

티치펜던트 화면에 문자열을 출력하는 간단한 job 프로그램을 작성해봅시다. 새로운 job을 생성한 후, 아래와 같이 [print문](../6-external-comm/3-tp-console-bar/1-print.md)을 기록하고, "Hello, World !"라는 문자열 파라미터를 붙입시다.

```python
print "Hello, World !"
```

print명령문은 티치펜던트의 job panel 하단에 값을 출력할 때 사용합니다. 이제 프로그램을 실행하면 job panel 하단에 Hello, World라는 문자열이 출력되는 것을 볼 수 있습니다.

# 2.5 자료형 \(type\)

# 2.5.1 문자열 자료형

앞 절의 첫 프로그램에서 print 문의 파라미터로서 "Hello, World" 라는 데이터를 사용했는데 이것은 문자열 자료형입니다. 문자열 자료형의 값은 큰 따옴표로 시작하고 끝납니다. 문자열 길이의 제한은 없습니다.

```python
print "Welcome to the Robot World."
```

문자열 내의 따옴표 혹은 특수 문자를 표현하기 위해 역슬래시\(\\)로 시작하는 시퀀스가 사용됩니다. 이러한 시퀀스를 이스케이프\(escape\) 문자라고 합니다.

지원되는 이스케이프 문자는 아래 표와 같습니다.

|  |  |
| :--- | :--- |
| \" | 큰 따옴표 \(double quote\) |
| \\ | 역 슬래시 \(backslash\) |
| \t | 탭 \(tab\) |
| \n | 개행 문자 |

```python
print "Message:\nPlease, press \"OK\" button."

출력결과
Message:
Please, press "OK" button.
```



# 2.5.2 숫자 자료형

숫자 자료형은 정수나 실수를 보관합니다.숫자 자료형도 있습니다. print 문으로 출력해봅시다. 아래 예와 같이 print 문에 여러 개의 값을 쉼표\(,\)로 구분하여 나열하면, 각각의 값이 공백으로 구분되어 출력됩니다.

```python
280
3.141592
-99
print 280, -99
```

시스템 내부적으로는 정수와 실수를 따로 구분해서 처리합니다. 각각의 데이터 크기는 아래와 같습니다.

| 데이터 형 | 데이터 크기 \(바이트\) |
| :--- | :--- |
| 정수 \(integer\) | 4 |
| 실수 \(real\) | 8 |

# 2.5.3 bool 자료형

아래와 같은 논리, 비교연산의 결과로서 true\(참\)와 false\(거짓\)의 2가지 값만을 갖습니다.

```python
var x=true
print false and x
print 10 > 5
print 10 <= 5

출력결과
false
true
false
```



# 2.5.4 배열과 객체형

이외에도 배열\(array\)과 객체\(object\)형이 있습니다. 이 후, 4.1절과 4.2절에서 자세히 알아보겠습니다. 

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



# 2.7 2진수와 16진수

앞에서 예를 든 숫자형 값들은 모두 10진수로 해석됩니다. 2진수나 16진수 값도 표현할 수 있는데 아래와 같이 각각 0b와 0x접두어를 붙여주면 됩니다.

```python
var binary = 0b10010011
var hexadecimal = 0xFF4A38C0
```

# 2.8 연산자와 수식

아래의 예를 보면 숫자 값 500에 변수 margin을 더한 후 2로 나누어 height라는 변수에 대입하고 있습니다.

```python
var height, margin=10
height=(500+margin)/2
print height
```

height에는 수식의 결과 값인 255가 대입된 것을 print문으로 확인할 수 있습니다.

이와 같이 값이나 변수인 피연산자\(operand\)들을 다양한 연산자\(operator\)로 연결하여 수식\(expression\)을 작성할 수 있고 그 결과를 변수에 대입하거나, 명령문의 파라미터로 사용할 수 있습니다.



아래와 같이 덧셈과 곱셈을 괄호없이 쓰면 어떤 연산이 먼저 수행될까요? 덧셈, 뺄셈보다 곱셈, 나눗셈을 먼저 한다는 걸 알고 있지요? 이처럼 연산자들 사이에는 수행되는 순서가 있으며 이를 연산자 우선순위\(operator precedence\)라고 합니다. 곱셈의 우선순위가 덧셈보다 높기 때문에 뒤에 있지만 먼저 수행되는 것입니다.



print 10+10\*2



문자열에 대해서도 + 연산자를 사용하면 문자열들이 연결\(concatenate\)됩니다.



```python
var name="axis1", type="rotational"
print name + ":" + type
```

HRScript가 지원하는 연산자는 아래와 같습니다. 위에 있을수록 연산자 우선순위가 높습니다. \(즉, 먼저 수행됩니다.\)

<table>
  <thead>
    <tr>
      <th style="text-align:left">연산자</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">예</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">( )</td>
      <td style="text-align:left">괄호 (grouping)</td>
      <td style="text-align:left">(10+10)*2 ; 40</td>
    </tr>
    <tr>
      <td style="text-align:left">[ ]</td>
      <td style="text-align:left">배열 요소 접근</td>
      <td style="text-align:left">arr[3]</td>
    </tr>
    <tr>
      <td style="text-align:left">**</td>
      <td style="text-align:left">승 (exponentiation)</td>
      <td style="text-align:left">10**3 ; 1000</td>
    </tr>
    <tr>
      <td style="text-align:left">+x, -x</td>
      <td style="text-align:left">부호 (sign)</td>
      <td style="text-align:left">-300</td>
    </tr>
    <tr>
      <td style="text-align:left">*, /, mod</td>
      <td style="text-align:left">곱셈, 나눗셈, 나머지</td>
      <td
      style="text-align:left">300/3 ; 100, 8 mod 3 ; 2</td>
    </tr>
    <tr>
      <td style="text-align:left">+, -</td>
      <td style="text-align:left">덧셈, 뺄셈</td>
      <td style="text-align:left">300-100 ; 200</td>
    </tr>
    <tr>
      <td style="text-align:left">~</td>
      <td style="text-align:left">bitwise NOT</td>
      <td style="text-align:left">
        <p>~0b11010010
          <br />
        </p>
        <p>; 0b11111111111111111111111100101101
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&amp;</p>
        <p>^</p>
        <p>|</p>
        <p>&lt;&lt;</p>
        <p>&gt;&gt;</p>
      </td>
      <td style="text-align:left">
        <p>bitwise AND
          <br />
        </p>
        <p>bitwise XOR
          <br />
        </p>
        <p>bitwise OR
          <br />
        </p>
        <p>shift left
          <br />
        </p>
        <p>shift right (부호유지)
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>0b11010010 &amp; 0b11110000 ; 0xd0
          <br />
        </p>
        <p>0b11010010 ^ 0b11110000 ; 0x22
          <br />
        </p>
        <p>0b11010010 | 0b11110000 ; 0xf2
          <br />
        </p>
        <p>0b11010010 &lt;&lt; 2 ; 0b1101001000
          <br />
        </p>
        <p>0b11010010 &gt;&gt; 2 ; 0b00110100
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>&lt;, &lt;=, &gt;, &gt;=,
          <br />
        </p>
        <p>!=, ==
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>비교연산
          <br />
        </p>
        <p>!=는 다르다. ==는 같다.
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>30 &lt;= 29 ; false
          <br />
        </p>
        <p>response != &quot;ok&quot;
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">not x</td>
      <td style="text-align:left">논리연산 NOT</td>
      <td style="text-align:left">not error_state</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>and
          <br />
        </p>
        <p>or
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>논리연산 AND
          <br />
        </p>
        <p>논리연산 OR
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>height&gt;100 and invert==false
          <br />
        </p>
        <p>timeout or work_count&gt;3
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

피연산자가 수치나 bool값일 경우, 비교연산과 논리연산의 결과는 bool자료형이며, 나머지 연산의 결과 형은 숫자 자료형입니다.



bool형의 피연산자를 비교연산자 없이 그대로 쓰면, 그 값이 true와 같은지를 뜻합니다. 예를 들어 아래의 두 행은 의미가 같습니다.

```python
var result= timeout
var result= (timeout==true)
```



문자열에 대해 사용할 수 있는 연산자는 덧셈\(+\)과 비교연산\(!=, ==\), 대입연산\(=\)입니다. 문자열 덧셈은 피연산자 문자열들을 연결\(concatenate\)하며, 앞서 예를 보인 바 있습니다.

비교연산은 문자열이 다른지 같은지를 판단합니다.

```python
var response="ok"
print response=="ok"
print response=="ng"
```

간혹, 연산과정에서 피연산자의 자료형이 자동으로 바뀌는 경우도 있습니다.

논리연산자의 피연산자로 수치를 사용할 경우, 수치가 0이면 false, 0이 아니면 true로 간주합니다.

```python
var count_a=1, count_b=0, height=100
print count_a and height>99
print count_b and height>99
```

bitwise NOT과 shift left/right는 32bit 길이를 기반으로 계산합니다.

# 2.9 함수

각도 60° 를 radian값으로 변환하려면 어떻게 해야 할까요? 혹은, 변수 mystr이 담고 있는 문자열의 길이를 알아내려면 어떻게 해야 할까요?

HRScript는 매개변수로 입력을 받아 어떤 처리를 한 후 결과값을 리턴해주는 여러가지 함수\(function\)를 제공합니다.

함수는 아래와 같이 수식의 일부로서 사용할 수 있습니다.

```python
var dg=60, rd
rd=deg2rad(dg)

var limit=40, message="Input your code number"
var validity= len(message) < limit
```

HRScript에서 제공되는 함수의 목록은 아래와 같습니다. \(각 표는 이름 정렬순입니다.\)

# 2.9.1 수학 함수

<table style="text-align:left">
	<thead>
		<tr>
			<th>함수</th>
			<th>설명</th>
			<th>사용 예</th>
			<th>결과</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>abs(a)</td>
			<td>a의 절대값 (absolute) 을 리턴합니다.</td>
			<td>abs(-300)</td>
				<td>300</td>
		</tr>
		<tr>
			<td>acos(a)</td>
			<td>a의 arc cosine값을 radian 형식으로 리턴합니다.</td>
			<td>acos(0.5)</td>
			<td>1.0472</td>
		</tr>
		<tr>
			<td>asin(a)</td>
			<td>a의 arc sige 값을 radian 형식으로 리턴합니다.</td>
			<td>asin(0.5)</td>
			<td>0.5236</td>
		</tr>
		<tr>
			<td>atan(a)</td>
			<td>a의 arctangent 값을 radian 형식으로 리턴합니다.</td>
			<td>atan(0.5)</td>
			<td>0.4636</td>
		</tr>
		<tr>
			<td>atan2(a, b)</td>
			<td>y길이가 a, x길이가 b인 삼각형의 arctangent 값을 radian 형식으로 리턴합니다.</td>
			<td>atan2(2,1)</td>
				<td>1.1071</td>
		</tr>
		<tr>
			<td>ceil(x)</td>
			<td>x의 올림 값을 리턴합니다.</td>
			<td>
				ceil(3.1415)<br>
				ceil(-3.1415)
			</td>
				<td>
				4<br>
				-3
				</td>
		</tr>
		<tr>
			<td>cos(r)</td>
			<td>radian 형식의 a의 cosine 값을 리턴합니다.</td>
			<td>cos(3.1415)</td>
			<td>-1</td>
		</tr>
		<tr>
			<td>deg2rad(d)</td>
			<td>degree 형식의 d의 radian 값을 리턴합니다.</td>
			<td>deg2rad(-90)</td>
			<td>-1.570796</td>
		</tr>
		<tr>
			<td>dist(x, y)</td>
			<td>원점에서 (x, y) 좌표까지의 유클리드 거리를 리턴합니다.</td>
			<td>dist(3.5,10)</td>
			<td>10.59481</td>
		</tr>
		<tr>
			<td>floor(x)</td>
			<td>x의 내림 값을 리턴합니다.</td>
			<td>
				floor(3.1415)<br>
				floor(-3.1415)
			</td>
			<td>
				3<br>
				-4
			</td>
		</tr>
		<tr>
			<td>max(a, b)</td>
			<td>a와 b중 큰 값을 리턴합니다.</td>
			<td>max(-1.23, -3)</td>
			<td>-1.23</td>
		</tr>
		<tr>
			<td>min(a, b)</td>
			<td>a와 b중 작은 값을 리턴합니다.</td>
			<td>max(-1.23, -3)</td>
			<td>-3</td>
		</tr>
		<tr>
			<td>near(a, b[,e])</td>
			<td>실수값 a와 b의 차이가 e보다 작거나 같으면 1, 크면 0을 리턴합니다.</td>
			<td>
				near(0.005, 0.0058)<br>
				near(0.005, 0.006)<br>
				near(0.005, 0.006, 0.1)
			</td>
			<td>
				1<br>
				0<br>
				1<br>
			</td>
		</tr>
		<tr>
			<td>rad2deg(r)</td>
			<td>radian 형식의 r의 degree값을 리턴합니다.</td>
			<td>rad2deg(1.570796)</td>
			<td>90</td>
		</tr>
		<tr>
			<td>round(x)</td>
			<td>x의 반올림 값을 리턴합니다.</td>
			<td>
				round(3.1415)<br>
				round(3.7415)<br>
				round(-3.1415)<br>
				round(-3.7415)
			</td>
				<td>
				3<br>
				4<br>
				-3<br>
				-4
				</td>
		</tr>
		<tr>
			<td>sin(r)</td>
			<td>radian 형식의 r의 sine 값을 리턴합니다.</td>
			<td>sin(1.5*3.1415)</td>
			<td>-1</td>
		</tr>
		<tr>
			<td>sqr(a)</td>
			<td>a의 제곱근(square root)을 리턴합니다.</td>
			<td>
				sqr(16)<br>
				sqr(0)
			</td>
			<td>
				4<br>
				0
			</td>
		</tr>
		<tr>
			<td>tan(r)</td>
			<td>radian 형식의 r의 tangent 값을 리턴합니다.</td>
			<td>tan(3.141592/4)</td>
			<td>0.9999</td>
		</tr>
		<tr>
			<td>trunc(x)</td>
			<td>x의 소수점 이하를 버린 정수값을 리턴합니다.</td>
			<td>
				trunc(3.1415)<br>
				trunc(-3.1415)
			</td>
			<td>
				3<br>
				-3
			</td>
		</tr>
	</tbody>
</table>
# 2.9.2 문자열 함수

var str="hello, world"가 실행된 상태에서의 예

<table>
  <thead>
    <tr>
      <th style="text-align:left">함수</th>
      <th style="text-align:left">설명</th>
      <th style="text-align:left">사용 예</th>
      <th style="text-align:left">결과</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">bin(a)</td>
      <td style="text-align:left">수치 a의 2진 표현 문자열을
        리턴합니다</td>
      <td style="text-align:left">bin(0b0010)</td>
      <td style="text-align:left">&quot;10&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">chr(a)</td>
      <td style="text-align:left">ASCII코드 a인 문자를 문자열형으로
        리턴합니다.</td>
      <td style="text-align:left">chr(65)</td>
      <td style="text-align:left">&quot;A&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">double(s)</td>
      <td style="text-align:left">
        <p>실수 문자열s의 실수형값을
          리턴합니다.
          <br />
        </p>
        <p>(해석되는 위치까지만
          해석하고 나머지는 버림)
          <br
          />
        </p>
      </td>
      <td style="text-align:left">double(&quot;29.38E-2&quot;)</td>
      <td style="text-align:left">0.2938</td>
    </tr>
    <tr>
      <td style="text-align:left">hex(a)</td>
      <td style="text-align:left">수치 a의 16진 표현 문자열을
        리턴 합니다.</td>
      <td style="text-align:left">hex(0x7A2F)</td>
      <td style="text-align:left">&quot;7A2F&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">int(s)</td>
      <td style="text-align:left">
        <p>정수 문자열s의 정수형값을
          리턴합니다.
          <br />
        </p>
        <p>(해석되는 위치까지만
          해석하고 나머지는 버림)
          <br
          />
        </p>
      </td>
      <td style="text-align:left">
        <p>int(&quot;13.25&quot;)
          <br />
        </p>
        <p>int(&quot;29.38E-2&quot;)
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>13
          <br />
        </p>
        <p>29
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">left(s, n)</td>
      <td style="text-align:left">문자열 s의 앞부분 n개의
        문자로 된 문자열을 리턴합니다.</td>
      <td
      style="text-align:left">left(str, 3)</td>
        <td style="text-align:left">&quot;hel&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">len(s)</td>
      <td style="text-align:left">
        <p>s가 문자열이면 문자열의
          길이를 리턴합니다.
          <br />
        </p>
        <p>s가 배열이면 배열의 요소
          개수를 리턴합니다.
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>len(&quot;HELLO&quot;)
          <br />
        </p>
        <p>len([20, 30, 80])
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>5
          <br />
        </p>
        <p>3
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">mid(s, i, n)</td>
      <td style="text-align:left">문자열 s의 i번째 문자부터
        n개의 문자로 된 문자열을
        리턴합니다. (첫 문자 위치는
        0.)</td>
      <td style="text-align:left">mid(str, 3, 5)</td>
      <td style="text-align:left">&quot;lo, w&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">mirror(s)</td>
      <td style="text-align:left">문자열 s를 역전한 문자열을
        리턴합니다.</td>
      <td style="text-align:left">mirror(&quot;HELLO&quot;)</td>
      <td style="text-align:left">&quot;OLLEH&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">right(s, n)</td>
      <td style="text-align:left">문자열 s의 뒷부분 n개의
        문자로 된 문자열을 리턴합니다.</td>
      <td
      style="text-align:left">right(str, 3)</td>
        <td style="text-align:left">&quot;rld&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">str(a)</td>
      <td style="text-align:left">수치 a의 10진 표현 문자열을
        리턴합니다.</td>
      <td style="text-align:left">str(13.25)</td>
      <td style="text-align:left">13.250000</td>
    </tr>
    <tr>
      <td style="text-align:left">strops(s, p)</td>
      <td style="text-align:left">s문자열 내에 p문자열과
        일치하는 최초의 위치를
        리턴합니다.(첫 문자 위치는
        0. 없으면 -1.)</td>
      <td style="text-align:left">
        <p>strpos(str, &quot;llo&quot;)
          <br />
        </p>
        <p>strpos(str, &quot;hi&quot;)
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>2
          <br />
        </p>
        <p>-1
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>



# 2.9.3 날짜, 시간 함수

<table>
  <thead>
    <tr>
      <th style="text-align:left">함수</th>
      <th style="text-align:left">설명</th>
      <th style="text-align:left">사용 예</th>
      <th style="text-align:left">결과</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">date( )</td>
      <td style="text-align:left">
        <p>현재의 날짜를 문자열
          형으로 리턴합니다.
          <br />
        </p>
        <p>(YYYY-MM-DD형식)
          <br />
        </p>
      </td>
      <td style="text-align:left">date( )</td>
      <td style="text-align:left">&quot;2019-04-17&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">time( )</td>
      <td style="text-align:left">
        <p>현재의 시간을 문자열
          형으로 리턴합니다.
          <br />
        </p>
        <p>(HH:MM:SS형식)
          <br />
        </p>
      </td>
      <td style="text-align:left">time( )</td>
      <td style="text-align:left">&quot;08:48:14&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">timer( )</td>
      <td style="text-align:left">전원투입 시로부터 경과한
        시간을 초(sec) 단위로 리턴합니다.</td>
      <td
      style="text-align:left">timer( )</td>
        <td style="text-align:left">2796.37</td>
    </tr>
  </tbody>
</table>

# 2.9.4 생성자 함수

매개변수를 입력받아 새로운 객체를 생성하여 리턴해주는 함수입니다.



<table>
  <thead>
    <tr>
      <th style="text-align:left">함수</th>
      <th style="text-align:left">설명</th>
      <th style="text-align:left">사용 예</th>
      <th style="text-align:left">결과</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>Array(n)
          <br />
        </p>
        <p>Array(a, b, c)
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>요소 n개의 배열을 생성해
          리턴합니다. 요소의 초기값은
          0입니다.
          <br />
        </p>
        <p>인수를 2개 이상 지정하면
          다차원 배열이 생성됩니다.
          <br
          />
        </p>
        <p>&quot;<a href="../../array-object/array/">4.1 배열</a>&quot;을
          참조하십시오.
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>Array(900)
          <br />
        </p>
        <p>Array(3,4)
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>배열[900]
          <br />
        </p>
        <p>배열[3][4]
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Pose(요소)</td>
      <td style="text-align:left">
        <p>포즈 객체를 생성해 리턴합니다.
          <br
          />
        </p>
        <p>&quot;<a href="../../moving-robot/pose.md">5.1 포즈 (pose)</a>&quot;를
          참조하십시오.
          <br />
        </p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">포즈 객체</td>
    </tr>
    <tr>
      <td style="text-align:left">Shift(요소)</td>
      <td style="text-align:left">
        <p>시프트 객체를 생성해
          리턴합니다.
          <br />
        </p>
        <p>&quot;<a href="../../moving-robot/shift.md">5.2 시프트 (shift)</a>&quot;를
          참조하십시오.
          <br />
        </p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">시프트 객체</td>
    </tr>
  </tbody>
</table>

# 2.9.5 기타 함수



<table>
  <thead>
    <tr>
      <th style="text-align:left">함수</th>
      <th style="text-align:left">설명</th>
      <th style="text-align:left">사용 예</th>
      <th style="text-align:left">결과</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">cpo(crd, mode)
        <br />
      </td>
      <td style="text-align:left">
        <p>로봇이 취하고 있는 현재
          자세(current pose)를 crd좌표계로
          리턴합니다.
          <br />
        </p>
        <p>crd 인수로 사용할 수 있는
          값은 &quot;<a href="../../moving-robot/pose.md">5.1 포즈 (pose)</a>&quot;의
          표를 참조하십시오.
          <br />
        </p>
        <p>mode가 &quot;cmd&quot;이면 지령값,
          &quot;cur&quot;이면 현재값입니다.
          <br
          />
        </p>
        <p>crd, mode 파라미터를 생략 가능하며
          디폴트값은 각각 “base”,
          ”cur” 입니다.
          <br />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left">cpo(&quot;joint&quot;, &quot;cmd&quot;)
        <br />
      </td>
      <td style="text-align:left">로봇의 지령값을 축좌표계로
        보관하는 포즈*</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>mkucs(n,po)
          <br />
        </p>
        <p>mkucs(n,po1,po2
          <br />
        </p>
        <p>,po3)
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>n번 사용자좌표계 객체를
          생성하여 등록합니다.
          <br
          />
        </p>
        <p>&quot;<a href="../../moving-robot/ucs.md">5.5 사용자좌표계 (UCS ; User Coordinate System)</a>&quot;를
          참조하십시오.
          <br />
        </p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>0 : OK
          <br />
        </p>
        <p>&lt;0 : 에러코드
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">result()</td>
      <td style="text-align:left">일부 프로시져는 수행
        결과를 확인해야 할 경우가
        있습니다. 프로시져 수행
        직후 result( ) 함수를 호출하면,
        수행 결과를 리턴 받을
        수 있습니다.</td>
      <td style="text-align:left">result()</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

\* 포즈\(pose\)는 로봇의 자세 혹은 툴 끝의 위치를 나타내는 데이터형입니다. 이후의 "[5.1 포즈 \(pose\)](../../5-moving-robot/1-pose.md)"에서 자세히 설명합니다.

# 3. 제어문과 서브프로그램

# 3.1 주소 \(Address\)

순서대로 다음 행을 수행하지 않고 프로그램의 다른 위치로 이동하는 것을 분기\(branch\)라고 합니다. 주소란 분기의 목적지\(destination\) 입니다.주소를 정의하는 방법은 아래와 같이 3가지 형식이 있습니다.



<table>
  <thead>
    <tr>
      <th style="text-align:left">종류</th>
      <th style="text-align:left">형식</th>
      <th style="text-align:left">예</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">행번호 (line-number)</td>
      <td style="text-align:left">
        1~9999 의 정수입니다. 스텝(move)이 아닌 명령문의 왼쪽에 지정할 수 있습니다.
      </td>
      <td style="text-align:left">99</td>
    </tr>
    <tr>
      <td style="text-align:left">레이블 (label)</td>
      <td style="text-align:left">
        레이블은 명령문에 지정하는 것이 아니라 그 자체로 명령문입니다.<br>
        \* 뒤에 [식별자](2-identifier.md)를 붙인 형식입니다. 단 식별자의 길이는 128자 이하여야 합니다.
      </td>
      <td style="text-align:left">*timeout</td>
    </tr>
    <tr>
      <td style="text-align:left">스텝 번호 (step number)</td>
      <td style="text-align:left">
        스텝(move) 명령문에 자동으로 1씩 증가하며 매겨집니다.<br>
        S뒤에 스텝의 번호를 붙인 형식입니다. S1~S999까지 지정 가능합니다.
      </td>
      <td style="text-align:left">S15</td>
    </tr>
  </tbody>
</table>


아래의 예에서 두 번째 명령문의 10은 행번호이고, \*err_handle은 레이블, S12는 스텝 번호입니다.

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
  10 z_pos = (base_height+offset)*1.05
     # robot has to wait sensor2 input
     *err_handle
S12  move P,spd=80%,accu=1,tool=3
```
# 3.2 정지, 대기문

# 3.2.1 stop문

### 설명

프로그램을 정지시킵니다. 재기동하면 다음 행부터 계속 수행합니다.

### 문법

stop

### 사용 예

```python
if di9
  stop
endif
```



# 3.2.2 end문

### 설명

프로그램을 정지시킵니다. 연속 재생모드이거나 재기동하면 주 프로그램의 처음부터 다시 수행합니다.

### 문법

end

### 사용 예

```python
move p,spd=70%,accu=1,tool=0
move p,spd=70%,accu=1,tool=0
end
```



# 3.2.3 delay문

### 설명

지정한 시간 동안 대기한 후 다음 명령문으로 진행합니다.

### 문법

delay &lt;시간&gt;

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">시간</td>
      <td style="text-align:left">대기할 시간</td>
      <td style="text-align:left">
        <p>산술식</p>
        <p>0.1~60.0 sec</p>
      </td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
delay 3.5
```



# 3.2.4 wait문

### 설명

지정한 조건이 참이 될 때까지 대기한 후 다음 명령문으로 진행합니다.

### 문법

wait &lt;조건&gt;\[,&lt;제한시간&gt;,&lt;timeout 주소&gt;\]

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">조건</td>
      <td style="text-align:left">대기할 조건</td>
      <td style="text-align:left">조건식</td>
    </tr>
    <tr>
      <td style="text-align:left">제한시간</td>
      <td style="text-align:left">조건이 거짓일 경우 대기할
        최대 제한 시간 (timeout)</td>
      <td style="text-align:left">
        <p>산술식
          <br />
        </p>
        <p>0.1~60.0 sec
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">timeout 주소</td>
      <td style="text-align:left">제한시간 초과 시, 분기할
        주소</td>
      <td style="text-align:left">주소</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
wait sensor_ok
wait (sensor_ok and pos_ok),10,*timeout
```

# 3.3 분기문

조건없이 다른 주소로 분기합니다.

# 3.3.1 goto 문

### 설명

지정한 주소로 분기합니다.

### 문법

goto &lt;주소&gt;

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">주소</td>
      <td style="text-align:left">
        <p>분기할 주소</p>
        <p>행 번호인 경우 산술식도
          가능</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
goto 99
goto addr
goto *err_hdl
```



# 3.3.2 gosub~retsub 문

### 설명

gosub문을 만나면 지정한 주소로 분기합니다. retsub문을 만나면 gosub문 다음 위치로 복귀합니다.  
gosub를 여러 단계로 내포할 수도 있으며 내포 횟수의 제약은 없습니다.

### 문법

```python
gosub <주소>
...
end
  
<address>
...  
retsub
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">주소</td>
      <td style="text-align:left">
        <p>분기할 주소</p>
        <p>행 번호인 경우 산술식도 가능</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
var x=5
var y=6
var res
var sum=0
gosub *calc_dist1
gosub *calc_dist2
var total=sum
if near(total,18.8102)
  print "OK"
else
  print "NG"
endif
end
     
*calc_dist1
res=x*x+y*y
res=sqr(res)
gosub *calc_sum
retsub
     
*calc_dist2
res=x+y
gosub *calc_sum
retsub
     
*calc_sum
sum=sum+res
retsub
end
```
# 3.4 조건문

조건에 따라 특정한 동작을 수행하거나 수행하지 않을 수 있습니다.

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



# 3.4.4. 복문 if~elseif~else~endif문

### 설명

조건이 여러 개일 경우에는 아래와 같은 형태로 elseif문을 사용할 수 있습니다.

### 문법

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

### 사용 예

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



# 3.6 반복문

같은 동작을 여러 번 반복하고자 할 때 반복문을 사용합니다.

# 3.6.1 for~next문

### 설명

같은 동작을 반복하는 for~next문의 형식은 아래와 같습니다.

먼저 인덱스변수에 초기값이 대입됩니다. for문 아래의 명령문들을 수행하다가 next문을 만나면 인덱스변수가 증감값을 더하고 for문 지점부터 반복합니다. 인덱스변수가 종료값을 지나가면 반복이 종료됩니다.

step은 지정하지 않으면 1로 적용됩니다.

### 문법

```python
for <인덱스변수>=<초기값> to <종료값> [step <증감값>]
	<명령문>
	…
next
```

### 사용 예

for~next문을 이용하여 1부터 10까지를 sum에 누적하는 루틴의 예를 아래에 보였습니다. 반복이 종료되면 화면에는 11, 55가 출력될 것입니다.

```python
var idx
var sum=0
for idx=1 to 10
	sum=sum+idx
next
print idx, sum
end
```

# 3.7 call문, jump문과 서브프로그램

규모가 큰 로봇 작업 전체를 하나의 JOB 프로그램으로 작성하면, 프로그램이 크고 복잡해져서 기능을 추가하거나 문제점을 찾아 해결하기 어려워집니다.

프로그램의 유지보수성을 위해, 전체 프로그램을 구성하는 단위 작업들을 각기 서브프로그램으로 분리하는 것이 바람직합니다. 예를 들어, 센서와의 통신을 수행하는 루틴, 수신된 데이터로 툴 끝의 목표위치를 계산하는 루틴, 에러가 발생했을 때 적절한 메시지를 만들어 보고하는 루틴 등을 각각의 서브 프로그램으로 만들어 주 프로그램이 호출하게 하면, 프로그램의 전체 구조를 파악하기도 쉽고, 분리한 서브 프로그램을 다른 프로젝트에서 재활용하기에도 좋습니다.



# 3.7.1 call문

### 설명

HRScript에서 메인 프로그램\(main program\)과 서브 프로그램\(sub program\) 간의 형식 상의 큰 차이는 없습니다. 기동 버튼이나 신호로 처음 실행된 JOB은 주 프로그램이고, call 명령문에 의해 호출된 JOB은 모두 서브 프로그램입니다. 

### 문법

```python
call <JOB번호 혹은 파일이름, 사용자함수명> [,매개변수1,매개변수2,…]
```

call 뒤에 JOB 번호, 혹은 JOB파일이름\(확장자 제외\)이나 사용자함수명을 지정합니다. A라는 프로그램이 수행되다가 call B를 만나면 A의 수행은 중단되고, 서브프로그램인 B 프로그램(혹은 사용자함수)의 첫 명령문부터 수행이 계속됩니다. B 수행 중 end문이나 return 문을 만나면 호출했던 A 프로그램 call문의 다음 명령문 위치로 복귀하여 A의 수행을 계속하게 됩니다.

### 사용 예

아래는 call 문에 의한 서브프로그램 호출의 예와 그 결과입니다. 서브프로그램이 하는 일이 print문 1개 뿐이라 프로그램을 둘로 분리한 것이 의미없어 보이기는 하지만 뒤에서 좀 더 실제적인 예를 보이도록 하겠습니다.

* 사용자 함수를 호출하는 예는 [3.7.3 def](./3-def.md)를 참조하십시오.

<br>

```python
# 0001_main.job
print "main job start"
call 102_err
print "main job end"
end
```

```python
# 0102_err.job
print "sub-program"
end
```

<br>
결과

```python
main job start
sub-program
main job end
```
# 3.7.2 매개변수와 param문, return문

JOB 프로그램은 입력과 출력을 전달하는 통로\(channel\)로서 형식 매개변수를 사용합니다. 형식 매개변수는 JOB 프로그램의 가장 선두에 param 명령문으로 정의합니다.

아래 예에서 105번 JOB은 원점으로부터 좌표값\(x,y\)까지의 유클리드 거리를 구하여 len으로 리턴하는 서브 JOB으로서 dist2d라고 이름을 지었습니다.

<br>

```python
# 0001_main.job
var x,y
x=5
y=12.8
call 105_dist2d,x,y
var res=result()
print res
end
``` 

```python
# 0105_dist2d.job
# Calc. Euclide distance 2D
param x,y
var tmp

tmp=x*x+y*y
var len=sqr(tmp) # distance from origin
return len
```
<br>

결과
```python
13.742
```
<br>

1번 JOB에서 이 dist2d 서브 프로그램을 call 문으로 호출하고 있으며, 지역변수인 x, y를 전달하고 있습니다. dist2d  서브 프로그램 내에서 param문으로 정의한 ldX, ldY를 형식 매개변수\(formal parameter\)라고 하며, call 문에 전달한 x, y를 실 매개변수\(actual parameter\)라고 합니다.

dist2d 프로그램은 결과값을 return 문을 통해 외부로 전달하고 있습니다. 이 return값은 호출한 프로그램에서 result\(\) 함수를 호출하여 얻을 수 있습니다.

\(return문과 end문은 프로그램을 종료하고 주 프로그램으로 리턴한다는 점에서 동작이 같습니다. 다만 return문은 결과값을 인수로 지정할 수 있다는 점에서만 end문과 다릅니다.\)
# 3.7.3 def문 (사용자함수 정의)

V60.05-06부터

### 설명

def문으로 job 내에 사용자 함수를 정의하여 이를 call문으로 호출할 수 있습니다. def문은 param문과 유사하게 형식매개변수들의 리스트를 지정할 수 있습니다. call문이 전달한 실매개변수 값은 형식매개변수로 전달됩니다.
def문으로 정의한 함수의 실행은 return문이나 end문을 실행할 때 call문 다음 위치로 리턴합니다.

사용자 함수는 번호가 아닌 이름으로 호출하므로 서브프로그램보다 가독성이 좋으며, 관련된 여러 함수들을 하나의 서브프로그램에 그룹핑할 수 있어서 더 나은 프로젝트 구조를 만들어 줍니다. 


### 문법

```python
def <사용자 함수명> [,매개변수1[=디폴트값],매개변수2[=디폴트값],…]
```

def 뒤에 사용자 함수명을 지정합니다. 함수명은 [2.2 식별자](../../2-basic-syntax/2-identifier.md) 절에서 정의한 규칙을 따라야 합니다. 또한, 프로젝트 전역적으로 유일한 명칭이어야 합니다. 다른 함수명 혹은 다른 변수명과 중복되지 않도록 유의하십시오.
그 뒤에는 형식매개변수들을 지정합니다. 매개변수에는 디폴트값을 지정할 수도 있습니다. call 문에서 실매개변수를 생략하면, 해당 형식매개변수는 디폴트값으로 초기화됩니다. 특정 형식매개변수에 디폴트값을 지정하기 시작하면 반드시 마지막 매개변수까지 지정해줘야 합니다.

```python
# 형식매개변수 디폴트값 예
def set_work,mass,cx=0,cy=0,cz=0 # 적법한 예
def set_work,mass,cx=0,cy,cz     # 적법하지 않은 예
```

### 사용 예

아래는 call 문에 의한 사용자함수 호출의 예와 그 결과입니다. 이전 절에서 서브프로그램 설명을 위해 제시한 유클리드 거리 예제를 확장하여 이번에는 유클리드 거리와 맨해튼 거리를 각각 사용자함수로 정의해서 호출해봅시다.


```python
# 0001_main.job
var x,y
x=5
y=12.8

call euclid_dist,x,y
var res=result()
print "euclid=",res # 13.7419

call manhattan_dist,x,y
var res=result()
print "manhattan=",res # 17.8
end
```

```python
# 0008_dist.job

# Calc. Euclide distance 2D
def euclid_dist,x,y
var tmp
tmp=x*x+y*y
var len=sqr(tmp) # distance from origin
return len

# Calc. Manhattan distance 2D
def manhattan_dist,x,y
var len=x+y
return len
```

결과
```python
euclid= 13.7419
manhattan= 17.8
end
```
<br># 3.7.3 jump문

### 설명

jump 문의 형식은 아래와 같습니다. 

### 문법

```python
jump <JOB번호 혹은 파일이름> [,매개변수1,매개변수2,…]
```

형식이 call문과 완전히 동일하며 동작도 유사합니다.

유일한 차이점은 call 문은 end문에 의해서 주 프로그램으로 리턴하지만, jump문은 리턴하지 않는다는 점입니다.

### 사용 예

call문 설명에서 본 예제 프로그램을 jump문으로 바꾸어 실행해 보면 결과는 아래와 같습니다. 서브프로그램\(0102\_err\)의 end를 만났을 때, 동작 사이클이 종료됩니다. 다음 동작 사이클을 수행하면, 주 프로그램\(0001\)의 처음부터 수행됩니다.


```python
# 0001_main.job
print "main job start"
jump 102_err
print "main job end"
end
```

```python
# 0102_err.job
print "sub-program"
end
```

결과
```python
main job start
sub-program
```
# 3.8 지역변수와 전역변수
# 3.8.1 지역변수

### 설명

지금까지는 var문으로 정의한 지역변수의 예만으로 예제를 설명해왔습니다. 지역변수는 하나의 JOB 프로그램 내에서 var문에 의해 생성된 후, end문을 만나 프로그램이 종료되면 자동으로 소멸됩니다. 그리고 다른 프로그램에서는 값을 읽거나 쓸 수 없습니다.

### 사용 예

main\_v는 0001.job 내에서만 접근 가능한 지역변수이고, sub\_v는 내에서만 접근 가능한 지역변수입니다. 다른 프로그램에서 접근하려고 하면 에러가 발생합니다.

지역변수 x는 0001.job과 0107.job에서 모두 정의했습니다. 이름이 같지만 서로 다른 변수이기 때문에, 서브 프로그램 0107에서 값으로 5를 설정했지만, 메인 프로그램 0001로 리턴한 후에는 5가 아닌 3이 출력됩니다. 

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var main_v=10
          <br />
        </p>
        <p>var x=3
          <br />
        </p>
        <p>call 107
          <br />
        </p>
        <p>print main_v # ok
          <br />
        </p>
        <p>print sub_v # error
          <br />
        </p>
        <p>print x # 3이 출력됨.
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0107.job</td>
      <td style="text-align:left">
        <p>var sub_v=20
          <br />
        </p>
        <p>var x
          <br />
        </p>
        <p>print sub_v # ok
          <br />
        </p>
        <p>print main_v # error
          <br />
        </p>
        <p>x=5
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>



# 3.8.2 전역변수

### 설명

global로 정의하는 전역 변수는 모든 JOB프로그램에서 항상 접근할 수 있습니다. 한번 정의되면 메인 프로그램의 end문이나 R0 \[ENTER\] 조작에 의해 프로그램 사이클이 리셋되어도 소멸되지 않습니다.

### 사용 예

global x가 처음 수행되면 변수 x가 생성되면서 default값 0으로 초기화되고, 다음 행에서 1로 증가합니다. 다음 프로그램 사이클에서 global x가 다시 수행될 때 x는 이미 정의되어 있기 때문에 새로 정의되지 않고 값 1도 보존됩니다. 반면 global y=10 은 정의와 함께 대입을 수행하며 다음 프로그램 사이클에서 수행되면 y변수값이 10으로 재초기화됩니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>global x
          <br />
        </p>
        <p>x=x+1
          <br />
        </p>
        <p>call 107
          <br />
        </p>
        <p>print x, y # 4, 10
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0107.job</td>
      <td style="text-align:left">
        <p>global y=10
          <br />
        </p>
        <p>print x, y # 3, 10
          <br />
        </p>
        <p>x=x+1
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

따라서 전역변수를 프로그램 사이클 횟수를 위한 카운터로 활용하고자 할 때에는 정의와 함께 값을 대입해서는 안됩니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">틀린 교시</td>
      <td style="text-align:left">
        <p>global count=0
          <br />
        </p>
        <p>count=count+1
          <br />
        </p>
        <p>…
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">올바른 교시</td>
      <td style="text-align:left">
        <p>global count
          <br />
        </p>
        <p>count=count+1
          <br />
        </p>
        <p>…
          <br />
        </p>
        <p>end</p>
      </td>
    </tr>
  </tbody>
</table>

# 3.8.3 우선순위

동일한 이름을 가진 지역변수와 전역변수가 있을 때에는 지역변수에 우선적으로 접근합니다. 가령, 아래 0005.job이 수행되는 동안은 전역변수 x와 지역변수 x가 동시에 존재하게 되는데, 이 때 x값을 읽어보면 지역변수가 읽힙니다. 0005.job에서 0001.job으로 리턴한 후, x값을 읽어보면 전역변수만 존재하는 상태이므로 전역변수가 읽힙니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>global x=100
          <br />
        </p>
        <p>call 5
          <br />
        </p>
        <p>print x # 100
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0005.job</td>
      <td style="text-align:left">
        <p>var x=&quot;hello&quot;
          <br />
        </p>
        <p>print x # hello
          <br />
        </p>
        <p>end</p>
      </td>
    </tr>
  </tbody>
</table>

# 4. 배열과 객체

# 4.1 배열





# 4.1.1 배열

배열은 여러 개의 값을 하나의 이름으로 모아 저장해 놓고, 인덱스\(index\) 번호를 통해 접근하는 변수형입니다.

배열은 다른 변수처럼 var이나 global로 정의합니다. 배열의 정의와 접근 형식은 아래와 같습니다.

|  |  |
| :--- | :--- |
| 정의 | var 배열명 = \[ 값, 값, …\] |
| 접근 | 배열명\[인덱스\] |

배열을 구성하는 값들을 요소\(element\)라고 합니다. 위 배열 distances에는 총 5개의 요소가 있습니다. 인덱스는 0부터 시작합니다. distances의 0번 요소는 10, 1번 요소는 10.5 입니다.

배열의 특정 요소값을 읽거나 쓸 때는 아래와 같이 \[ \] 연산자를 사용합니다.

아래는 객체 정의하고 접근 한 예입니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var distances = [ 10, 10.5, 12.7, 11.92, 9.5 ]
          <br />
        </p>
        <p>distances[1]=20.5
          <br />
        </p>
        <p>print distances[0], distances[1]
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">
        <p>10
          <br />
        </p>
        <p>20.5</p>
        <p>
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

배열의 요소 개수는 len\( \) 함수로 얻을 수 있습니다. 앞에서 len\( \) 함수는 문자열의 길이를 얻는 함수로서 소개된 바 있습니다. 그런데, len\( \)의 매개변수로 배열을 넣으면 배열의 요소 개수를 리턴해줍니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
      <th style="text-align:left">결과</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">len(a)</td>
      <td style="text-align:left">
        <p>a가 문자열이면 문자열의
          길이를 리턴합니다.
          <br />
        </p>
        <p>a가 배열이면 배열의 요소
          개수를 리턴합니다.
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>len(&quot;HELLO&quot;)
          <br />
        </p>
        <p>len([20, 30, 80])
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>5</p>
        <p>3</p>
      </td>
    </tr>
  </tbody>
</table>

배열의 모든 요소들에 대해 어떤 처리를 수행하는 경우에는 주로 for~next 문이 사용됩니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var distances = [ 10, 10.5, 12.7, 11.92, 9.5]
          <br />
        </p>
        <p>for i=0 to len(distances)-1
          <br />
        </p>
        <p>distances[i] = distances[i]+10
          <br />
        </p>
        <p>print distances[i]
          <br />
        </p>
        <p>next
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">
        <p>20
          <br />
        </p>
        <p>20.5
          <br />
        </p>
        <p>22.7
          <br />
        </p>
        <p>21.92
          <br />
        </p>
        <p>19.5
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

배열 안에 저장되는 값들은 서로 다른 타입이어도 상관없습니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var arr = [ 10, &quot;abc&quot;, true]
          <br />
        </p>
        <p>for i=0 to 2
          <br />
        </p>
        <p>print arr[i]
          <br />
        </p>
        <p>next
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">
        <p>10
          <br />
        </p>
        <p>abc
          <br />
        </p>
        <p>true
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>



# 4.1.2 다차원 배열

배열의 요소로서 배열이 내포될 수도 있습니다.

다차원 배열의 요소에 접근할 때는 \[ \] 연산자를 연속적으로 사용하면 됩니다.

아래의 예에서 arr\_y는 2차원 배열입니다. \(1\)

arr\_y\[1\]는 이 중 인덱스 1의 요소, 즉 \["abc", "jqk", "xyz"\] 배열인데, 이를 새로운 변수 arr\_x에 대입했습니다. \(2\)

따라서, arr\_x\[1\]은 "jqk"이고, arr\_y\[1\]\[2\]는 arr\_y\[1\]의 \[2\]를 가리키므로 "xyz"입니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var arr_y = [ [10,20], [&quot;abc&quot;,&quot;jqk&quot;, &quot;xyz&quot;]
          ] # (1)
          <br />
        </p>
        <p>var arr_x=arr_y[1] # (2)
          <br />
        </p>
        <p>print arr_x[1]
          <br />
        </p>
        <p>print arr_y[1][2]
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">
        <p>jqk
          <br />
        </p>
        <p>xyz
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

# 4.1.3 배열 생성자 함수

수 백개의 요소를 가진 배열을 생성하고자 한다면, \[ \] 표기만으로는 어렵습니다. 생성자 함수를 호출하면 원하는 개수의 배열을 생성할 수 있습니다. 각 요소는 0으로 초기화됩니다.

```python
var 배열변수명 = Array(900)	# 900개의 요소를 가진 배열 생성
```

인수를 2개 이상 지정하면 다차원 배열을 생성할 수 있습니다. 아래 3차원 배열의 예에서는 \[4\]가 최하위 차원\(dimension\)입니다.

```python
var 배열변수명 = Array(3,2,4)	# [3][2][4]개의 3차원 배열 생성
# [ [[0,0,0,0], [0,0,0,0]], [[0,0,0,0], [0,0,0,0]], [[0,0,0,0], [0,0,0,0]] ]
```



# 4.2 객체 \(object\)

앞서, 배열은 여러 개의 요소값을 보관할 수 있고, 인덱스로 접근한다는 것을 배웠습니다.

객체는 여러 요소 값을 보관한다는 점에서는 배열과 같습니다. 다른 점은 인덱스가 아닌 키\(key\)로 접근한다는 점입니다. 키는 숫자가 아닌 문자열입니다.

객체는 다른 변수처럼 var이나 global로 정의합니다. 객체의 정의와 접근 형식은 아래와 같습니다.



|  |  |
| :--- | :--- |
| 정의 | var 객체명 = { 키 : 값, 키 : 값, …} |
| 접 | 객체명.키 |

아래는 객체 정의하고 접근 한 예입니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var gap = { x:200, y:152.6 }
          <br />
        </p>
        <p>gap.x = gap.x + 10
          <br />
        </p>
        <p>print gap.x, gap.y
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">210 152.6</td>
    </tr>
  </tbody>
</table>

객체의 키는 반드시 식별자 형식이어야 하지만, 요소의 값은 모든 타입이 허용되며 서로 다른 타입이어도 상관없습니다.

객체는 요소로서 다른 객체나 배열을 포함할 수 있습니다. 마찬가지로 배열도 요소로서 다른 배열이나 객체를 포함할 수 있습니다. 아래 예에서, 객체 work는 객체 size와 배열 heights를 포함하고 있습니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var work = { part_no:3, name: &quot;gear&quot;, tested : false
          <br />
        </p>
        <p>, size : { x : 150, y : 80 }
          <br />
        </p>
        <p>, heights : [ 72.89, 74.91, 81.03, 87.60, 87.11 ] }
          <br />
        </p>
        <p>print work.tested, work.size.y, work.heights[3]
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>

      <td style="text-align:left">false, 80, 87.600000</td>
    </tr>
  </tbody>
</table>

# 4.3 배열과 객체의 복사 대입\(assignment\)

대입문 우변이 배열이나 객체 변수인 경우, 변수의 값 전체가 좌변의 변수로 복사됩니다. 배열이나 객체가 요소값으로서 서브 배열과 서브 객체들을 복잡하게 포함하고 있을 때에도, 이러한 포함 구조들이 모두 복사되는데 이를 깊은 복사\(deep copy\)라고 합니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var my_obj = { x:5, y:0, z:0 }
          <br />
        </p>
        <p>my_obj.y=[ [10, 20], [&quot;abc&quot;, true] ]
          <br />
        </p>
        <p>my_obj.z={ a:7, b:8 }
          <br />
        </p>
        <p>var your_obj=my_obj # deep copy
          <br />
        </p>
        <p>print your_obj.y[0]
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">[10, 20]</td>
    </tr>
  </tbody>
</table>

![](../_assets/image.png)



# 4.4 참조 전달\(call-by-reference\)과 값 전달\(call-by-value\)

3.4절의 call문과 jump문 설명에서 형식 매개변수와 실 매개변수의 개념을 배운 바 있습니다. 실 매개변수를 서브 프로그램으로 전달했는데, 서브 프로그램이 이 변수의 값을 변경한 후 종료했다면 변경된 내용이 메인 프로그램에 반영되어 있을까요?

가령, 아래와 같이 세제곱을 해주는 서브 프로그램 0005\_pow3.job를 만들었다고 합시다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var x=2
          <br />
        </p>
        <p>call 0005_pow3,x
          <br />
        </p>
        <p>print x
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0005_pow3.job</td>
      <td style="text-align:left">
        <p>param p
          <br />
        </p>
        <p>var t=p
          <br />
        </p>
        <p>p=t*t*t # (1)
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">2</td>
    </tr>
  </tbody>
</table>

2\*2\*2는 8이므로 8이 출력되기를 기대했지만, 결과는 2입니다. 숫자형 실 매개변수가 서브 프로그램으로 전달될 때는 매개변수로 값\(value\)이 복사되기 때문입니다. \(1\)에서 세제곱 값을 복사본에 대입한 것이므로 원본 변수 x의 값에는 영향을 주지 못한 것입니다.

따라서, 아래와 같이 return문으로 결과값을 전달받도록 교시 프로그램을 고쳐야 합니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var x=2
          <br />
        </p>
        <p>call 0005_pow3,x
          <br />
        </p>
        <p>x=result()
          <br />
        </p>
        <p>print x
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0005_pow3.job</td>
      <td style="text-align:left">
        <p>param p
          <br />
        </p>
        <p>var t=p
          <br />
        </p>
        <p>p=t*t*t
          <br />
        </p>
        <p>return p
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">8</td>
    </tr>
  </tbody>
</table>

반면, 배열이나 객체의 경우에는 복사본이 아니라 실제 변수의 참조\(reference\)가 전달됩니다. 참조란 변수의 위치와 같은 개념입니다.



아래와 같이 배열의 각 요소를 세제곱 해주는 서브 프로그램 0006\_pow3.job의 경우에는 의도한 대로 실 매개변수 배열의 요소 값들이 변경되었습니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left"></th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0001.job</td>
      <td style="text-align:left">
        <p>var x=[3, 2, 4]
          <br />
        </p>
        <p>call 0006_pow3,x
          <br />
        </p>
        <p>print x
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">0006_pow3.job</td>
      <td style="text-align:left">
        <p>param p
          <br />
        </p>
        <p>var t
          <br />
        </p>
        <p>for i=0 to len(arr)-1
          <br />
        </p>
        <p>t=p[i]
          <br />
        </p>
        <p>p[i] = t*t*t
          <br />
        </p>
        <p>next
          <br />
        </p>
        <p>end
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">결과</td>
      <td style="text-align:left">[27, 8, 64]</td>
    </tr>
  </tbody>
</table>

서브 프로그램 호출 시, 실 매개변수의 값의 복사본이 전달되는 것을 값에 의한 호출\(call-by-value\), 참조가 전달되는 것을 참조에 의한 호출\(call-by-reference\) 이라고 합니다. 값 호출일 지 참조 호출일 지는 아래와 같이 값의 형\(type\)에 의해 결정됩니다.

|  |  |
| :--- | :--- |
| 값에 의한 호출 | bool형, 숫자형, 문자열형 |
| 참조에 의한 호출 | 배열형, 객체형 |

![](../_assets/image_3.png)



# 5. 로봇언어로 로봇 움직이기

로봇의 목표위치를 표현하는 포즈를 이해한 후, 로봇 이동 명령을 배워봅시다.

# 5.1 포즈 \(pose\)

포즈는 hi6 제어기에 기본 내장된 객체형으로서, 로봇의 각 축의 자세, 혹은 툴 끝의 직교좌표와 방향을 표현합니다.

포즈는 생성자 함수 Pose\( \)를 호출하여 생성합니다. 함수 매개변수들은 모두 위치 매개변수입니다. crd와 cfg는 문자열형이고, 나머지는 모두 숫자형입니다.

{% hint style="info" %}
cfg요소는 로봇 자세 \(configuration\)를 지정합니다. 자세한 내용은 Hi6 로봇제어기 조작설명서의 "[2.3.2.2 베이스 및 로봇 기록 좌표](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/2-operation/3-step/2-step-pose-modify/2-base-robot-crd-sys)"를 참조하십시오.

{% endhint %}

```python
var 포즈변수명 = Pose(j1, j2, j3, …)					# 축 좌표
var 포즈변수명 = Pose(x, y, z, rx, ry, rz, j7, j8,…, crd, cfg)		# base 좌표
```

6축+부가1축, 직교+부가 1축의 포즈를 생성하는 아래의 예를 참고하십시오.

```python
var po1 = Pose(10, 90, 0, 0, -30, 0, -1240.8)				# 축 좌표
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, -1240.8, "base", "fl;r2")	# base 좌표
```

혹은, 1개의 배열 혹은 문자열 매개변수로도 Pose 생성자 함수를 호출할 수 있습니다. 이를 활용해, 파일이나 원격통신으로 얻은 데이터를 포즈로 변환해 사용할 수 있습니다.

```python
var 포즈변수명 = Pose(array)
var 포즈변수명 = Pose(string)
```

아래의 예를 참고하십시오.

```python
var arr = [10, 90, 0, 0, -30, 0, -1240.8]
var str = "[1850, 0, 2010.5, 0, -90, 0, -1240.8, \"base\", \"fl;r2\"]"
var po3 = Pose(arr)
var po4 = Pose(str)
```

Pose 객체의 요소들은 다음의 키들로 접근 가능합니다.

<!--![](../_assets/image_5.png)-->

<table>
  <tr>
    <th>키</th>
    <th>타입</th>
    <th>값 범위</th>
    <th>설명</th>
    <th>단위, 비고</th>
  </tr>
    <tr>
    <td>nj</td>
    <td>정수형</td>
    <td>1~32</td>
    <td>축 개수</td>
    <td> </td>
  </tr>
   </tr>
    <tr>
    <td>j1~j32</td>
    <td>실수형</td>
    <td>8 바이트 실수 범위</td>
    <td>축 값</td>
    <td>mm, deg</td>
  </tr>
   </tr>
    <tr>
    <td>x, y, z</td>
    <td>실수형</td>
    <td>8 바이트 실수 범위</td>
    <td>직교좌표 값</td>
    <td>mm</td>
  </tr>
   </tr>
    <tr>
    <td>rx, ry, rz</td>
    <td>실수형</td>
    <td>8 바이트 실수 범위</td>
    <td>좌표계 방향 오일러 각도</td>
    <td>deg</td>
  </tr>
  <tr>
    <td rowspan="4">crd</td>
    <td rowspan="4">문자열형</td>
    <td>joint</td>
    <td>축 좌표계 (default)</td>
    <td rowspan="4"></td>
  </tr>
  <tr>
    <td>base</td>
    <td>베이스 좌표계</td>
  </tr>
  <tr>
    <td>robot</td>
    <td>로봇 좌표계</td>
  </tr>
  <tr>
    <td>u1 ~ u10</td>
    <td>사용자 좌표계</td>
  </tr>
  <tr>
    <td rowspan="8">cfg</td>
    <td rowspan="8">문자열형</td>
    <td>s</td>
    <td>|S|>=180</td>
    <td rowspan="7">; 으로 구분하여,<br> 조합가능 <br> default 는 모든 flag 꺼짐.</td>
  </tr>
  <tr>
    <td>r1</td>
    <td>|R1|>=180</td>
  </tr>
  <tr>
    <td>r2</td>
    <td>|R2|>=180</td>
  </tr>
  <tr>
    <td>b</td>
    <td>|B|>=180</td>
  </tr>
  <tr>
    <td>re</td>
    <td>rear</td>
  </tr>
  <tr>
    <td>dn</td>
    <td>down</td>
  </tr>
  <tr>
    <td>nf</td>
    <td>non-flip</td>
  </tr>
  <tr>
    <td>auto</td>
    <td>auto (자동 결정)</td>
    <td></td>
  </tr>
</table>


아래의 예와 같이 포즈 요소값에 접근할 수 있습니다.

```python
po1.j2 = po1.j2 + 5
print po2.z, po2.cfg
```



# 5.2 시프트 \(shift\)

시프트는 hi6 제어기에 기본 내장된 객체형으로서, 포즈에 대한 변경값을 표현합니다.

시프트는 생성자 함수 Shift\( \)를 호출하여 생성합니다. 함수 매개변수들은 모두 위치 매개변수입니다. crd와 cfg는 문자열형이고, 나머지는 모두 숫자형입니다.

```python
var 시프트변수명 = Shift(j1, j2, j3, …)				# 축 좌표
var 시프트변수명 = Shift(x, y, z, rx, ry, rz, j7, j8,…, crd)		# base 좌표
```

6축+부가1축, 직교+부가 1축의 시프트를 생성하는 아래의 예를 참고하십시오.

```python
var sft1 = Shift(30, 0, 0, 0, -5.8, 0, -120)				# 축 좌표
var sft2 = Shift(0, 0, 55.2, 0, -5, 0, -120, "base")			# base 좌표
```

혹은, 1개의 배열 혹은 문자열 매개변수로도 Shift 생성자 함수를 호출할 수 있습니다. 이를 활용해, 파일이나 원격통신으로 얻은 데이터를 시프트로 변환해 사용할 수 있습니다.

```python
var 시프트변수명 = Shift(array)
var 시프트변수명 = Shift(string)
```

아래의 예를 참고하십시오.

```python
var arr = [30, 0, 0, 0, -5.8, 0, -120]
var str = "[0, 0, 55.2, 0, -5, 0, -120, \"base\"]"
var sft3 = Shift(arr)
var sft4 = Shift(str)
```

Shift 객체의 요소들은 다음의 키들로 접근 가능합니다.

![](../_assets/image_4.png)

# 5.3 포즈식 \(pose expression\)

결과값이 포즈가 되는 수식을 포즈식이라고 합니다.

아래와 같은 형태가 모두 포즈식으로 인식됩니다.



```python
포즈
포즈+시프트
포즈-시프트
포즈+시프트+시프트+…
```

포즈식의 결과를 다른 포즈 변수에 대입하는 아래의 예를 참고하십시오.

```python
var po1 = Pose(10, 90, 0, 0, -30, 0)
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, "base", "fl;r2")
var po3 = cpo("robot")
var sft1 = Shift(30, 0, 0, 0, -5.8, 0)
var po4 = po1-sft1
var po5 = po2+sft1+Shift(0, 0, 55.2, 0, -5, 0, "base")
```

# 5.4 move문

move문은 로봇을 움직이는 프로시져입니다. 형식은 아래와 같습니다.

### 설명

로봇의 툴 끝이 포즈 위치로 이동합니다.

### 문법

move &lt;보간&gt;, \[tg=&lt;포즈/시프트&gt;\], spd=&lt;속도&gt;, accu=&lt;정밀도&gt;

, tool=&lt;툴 번호&gt; \[until &lt;조건식&gt;\]

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">보간</td>
      <td style="text-align:left">
        <p>P : 축보간, L : 직선보간, C
          : 원호보간
          <br />
        </p>
        <p>SP: 정치툴 축보간, SL: 정치툴
          직선보간,
          <br />
        </p>
        <p>SC: 정치툴 원호보간
          <br />
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>포즈/</p>
        <p>시프트</p>
      </td>
      <td style="text-align:left">
        <p>이동할 목표(target) 자세 (포즈).
          <br
          />
        </p>
        <p>숨은 포즈가 있으면 생략됩니다.
          <br
          />
        </p>
        <p>+나 – 부호를 붙인 시프트식을
          지정하면 (숨은포즈+시프트식)이
          목표 자세로 적용됩니다.
          <br
          />
        </p>
      </td>
      <td style="text-align:left">
        <p>포즈식</p>
        <p>혹은</p>
        <p>부호 시프트식
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">속도</td>
      <td style="text-align:left">
        <p>툴 끝의 이동속도.
          <br />
        </p>
        <p>단위(mm/sec, cm/min, sec, %)를 붙여야
          합니다.
          <br />
        </p>
      </td>
      <td style="text-align:left">산술식.</td>
    </tr>
    <tr>
      <td style="text-align:left">정밀</td>
      <td style="text-align:left">산술식. 낮을수록 정밀함.
        0이면 불연속으로 동작</td>
      <td
      style="text-align:left">0~7</td>
    </tr>
    <tr>
      <td style="text-align:left">툴 번호</td>
      <td style="text-align:left">로봇 동작 시 사용할 툴의
        번호.</td>
      <td style="text-align:left">0~31</td>
    </tr>
    <tr>
      <td style="text-align:left">조건식</td>
      <td style="text-align:left">
        <p>조건식이 참인 순간 로봇동작이
          종료되고 지정한 포즈에
          도달한 것으로 간주합니다.
          <br
          />
        </p>
        <p>조건식의 결과는 result( ) 함수로
          얻을 수 있습니다.
          <br />
        </p>
      </td>
      <td style="text-align:left">
        <p>0이 아니면 참
          <br />
        </p>
        <p>0이면 거짓
          <br />
        </p>
      </td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
move L,tg=po[0]+sft[1],spd=800mm/sec,accu=0,tool=1
move P,tg=+Shift(0,0,0,0,-10,0),spd=80%,accu=1,tool=3 until di2  (숨은 포즈)
if result() then *sensor_on
```

티치펜던트의 \[기록\] 버튼을 누르면 현재로봇 자세로 숨은 포즈 방식의 move문이 기록됩니다. 숨은 포즈의 값은 move 문에 커서를 두고 \[속성\] 버튼을 눌러 확인하거나 편집할 수 있습니다.

\[명령입력\] 버튼을 누르고 \[모션\] 그룹을 연 후 move 메뉴를 선택하면, 포즈 방식의 move문이 기록됩니다.



# 5.5 mkucs함수 - 사용자좌표계

### 설명

세 개의 포즈 혹은 한 개의 포즈로 사용자좌표계를 생성하는 명령어입니다.   

- 세 개의 포즈로 생성시 원점포즈, X축포즈, XY평면포즈로 사용자 좌표계를 생성합니다.
- 한 개의 포즈로 생성시 원점포즈로 사용자 좌표계를 생성하며 위치/방향은 해당 포즈 값을 기준으로 생성합니다.
- 계산할 수 없는 경우, 에러가 발생하면서 job 실행이 중단됩니다.


### 문법

```python
<결과변수> = mkucs(<사용자좌표계 번호>,<원점포즈>,<X방향포즈>,<XY평면포즈>)
또는
<결과변수> = mkucs(<사용자좌표계 번호>,<원점포즈>)
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">결과변수</td>
      <td style="text-align:left">
        백그라운드 수행 결과<br>
        <ul>
        <li>0: 성공적으로 완료됨.</li>
        <li>-1: 사용자 좌표계 생성 실패함.</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">사용자좌표계 번호</td>
      <td style="text-align:left">
        생성할 사용자좌표계의 번호
      </td>
      <td style="text-align:left">[1~20]</td>
    </tr>
    <tr>
      <td style="text-align:left">원점포즈</td>
      <td style="text-align:left">
        원점에 위치한 포즈
      </td>
      <td style="text-align:left">포즈변수</td>
    </tr>
    <tr>
      <td style="text-align:left">X방향포즈</td>
      <td style="text-align:left">
        X축에 위치한 포즈
      </td>
      <td style="text-align:left">포즈변수</td>
    </tr>
    <tr>
      <td style="text-align:left">XY평면포즈</td>
      <td style="text-align:left">
        XY 평면에 위치한 포즈
      </td>
      <td style="text-align:left">포즈변수</td>
    </tr>
  </tbody>
</table>

### 리턴값


<table>
  <thead>
    <tr>
      <th style="text-align:left">값</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>
        성공
      </td>
      <td></td>
    </tr>  
  </tbody>
</table>


### 에러 가이드

- E14613 : 티칭 된 포즈의 개수가 부족할때 발생합니다. 1개 혹은 3개의 포즈를 입력하여 주십시오.
- E14614 : 사용자좌표번호가 숫자가 아닐때 발생합니다. 사용자좌표번호를 다시 지정하십시오.
- E14615 : 사용자좌표번호가 1~20 사이의 숫자가 아닐 때 발생합니다. 사용자좌표번호를 변경하십시오.
- E1011 : 티칭 된 포즈간 거리가 너무 가까울때 발생합니다. 각 점간 거리가 1mm이하일 때 발생합니다. 포즈간 거리값을 수정하여 주십시오.
- E1012 : 티칭 된 세 개의 포즈가 일직선상에 있을때 발생합니다. 


### 사용 예

```python
   var p_origin=Pose(0,0,0,0,0,0,"base")
   var p_xaxis=Pose(100,0,0,0,0,0,"base")
   var p_xyplane_=Pose(100,100,0,0,0,0,"base")
   var uc1 = mkucs(1,p_origin,p_xaxis,p_xyplane)
   var uc2 = mkucs(2,p_origin)
   end
```

![](../../_assets/mkucs.png)

# 5.6 selucrd문

selucrd문은 조건설정의 사용자 좌표계로 지정되어 있는 사용자 좌표계 번호를 변경하기 위한 프로시져입니다.

### 설명

조건설정의 사용자(User) 좌표계 지정에 해당하는 기능입니다.


### 문법

```python
selucrd <좌표계번호>
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">좌표계 번호</td>
      <td style="text-align:left">
        선택할 사용자 좌표계 번호<br>
        <ul>
        <li>0: 사용자 좌표계 지정 해제</li>
        <li>1~20: 사용자 좌표계 지정</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
   selucrd 1
   end
```# 5.6 contpath문

### 설명

CONTPATH(연속패스)의 모드를 선택합니다.

CONTPATH에 대한 설명은 아래 링크를 참조하십시오.  
[조작설명서: 8.15 R360 CONTPATH 수동 설정](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/8-r-code/15-r360)
<br><br>


### 문법

```python
contpath <모드 번호>
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">모드 번호</td>
      <td style="text-align:left">
        0: 불연속<br>
        1: 연속. 단, 입력신호는 불연속 (default)<br>
        2: 연속. 입력신호도 연속
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
contpath 0
contpath 1
contpath 2
```


{% hint style="info" %}

-	`contpath`문을 명시적으로 실행하지 않으면, 디폴트로 `contpath 1`이 적용됩니다. 명시적으로 지정한 경우에도 사이클 시작 시에는 `contpath 1` 로 초기화됩니다.

- 변경된 상태는 제목표시줄의 `CP0` / `CP1` / `CP2` 플래그로 확인할 수 있습니다.

{% endhint %}# 6. 외부장치와 통신하기

# 6.1 fb객체 : 디지털 I/O

HRScript에서 접근할 수 있는 총 10개의 fb객체를 통해 디지털 I/O 입출력을 할 수 있습니다. fb는 Fieldbus Block이라는 의미이며, 각 fb 객체는 로봇제어기에 장착된 I/O 하드웨어에 매핑되도록 설정되며, 출력변수와 입력변수들을 요소로서 포함하고 있습니다.

# 6.1.1 입출력 변수

![](../../_assets/image_1_1.png)

do, dob, dow, dol, dof에서 접미사 b, w, l, f는 각기 byte, word, long, float를 뜻하며 모두 부호있는 값\(signed value\)입니다. 이들은 별개의 메모리 공간이 아니라 같은 960 bit의 공간을 서로 다른 데이터형으로 표현한 것입니다. 예를 들어 do\[0~15\]와 dob\[0~1\], dow\[0\]은 모두 동일한 출력신호입니다. 인덱스는 do는 bit단위, dob, dow, dol, dof는 byte단위로 매겨집니다.

![](../../_assets/image_2.png)

do로 시작하는 출력변수에 값을 대입하면, I/O신호 출력이 수행됩니다. 현재, 입력되고 있는 I/O신호값은 di로 시작하는 입력변수값을 읽어 얻을 수 있습니다.

do변수는 읽기, 쓰기가 모두 가능하지만, di변수는 읽기만 가능합니다.



fb 객체명은 아래와 같이 생략할 수도 있습니다.

| **객체명** | **do 표기** | fb.do 표기 |
| :--- | :--- | :--- |
| fb0 | do0 ~ do959 | fb0.do0 ~ fb0.do959 |
| fb1 | do960 ~ do1919 | fb1.do0 ~ fb1.do959 |
| fb2 | do1920 ~ do2879 | fb2.do0 ~ fb2.do959 |
| fb3 | do2880 ~ do3839 | fb3.do0 ~ fb3.do959 |
| fb4 | do3840 ~ do4799 | fb4.do0 ~ fb4.do959 |
| fb5 | do4800 ~ do5759 | fb5.do0 ~ fb5.do959 |
| fb6 | do5760 ~ do6719 | fb6.do0 ~ fb6.do959 |
| fb7 | do6720 ~ do7679 | fb7.do0 ~ fb7.do959 |
| fb8 | do7680 ~ do8639 | fb8.do0 ~ fb8.do959 |
| fb9 | do8640 ~ do9599 | fb9.do0 ~ fb9.do959 |



# 6.1.2 예제

아래의 사용 예를 참고하십시오.

```python
do2=1			# fb0의 2번 비트출력값 켠다.
fb2.dob3=0b00001111  	# fb2의 3번 바이트출력값을 2진 bit열로 지정
fb[4].dob1=0x0F  	# fb4의 1번 바이트출력값 하위 4비트를 켜고, 상위 4비트를 끈다.
var work_no=fb9.dib3    # fb9의 3번 바이트입력값을 work_no 변수에 대입
if fb5.di43 then *err  	# fb5.di42가 켜지면 *err 레이블로 분기
for idx=21 to 29
  fb3.do[idx]=1  	# fb3의 출력신호 do21 ~ do29를 모두 켠다. 
next
fb2.do3=fb2.do7=fb2.do11=1   # fb2의 3번, 7번, 11번 출력신호를 한꺼번에 켠다.
```

# 6.1.3 pulse문

pulse문은 펄스 형태의 신호 출력을 위해 사용하는 프로시져 입니다.

### 설명

tlag 시간 후에, ton 시간 동안 On(High), toff 시간 동안 Off(Low) 형태의 펄스가 cnt 횟수만큼 출력됩니다.


### 문법

```python
pulse <신호>,tlag=<지연 시간>,ton=<On 시간>,toff=<Off 시간>,cnt=<출력 횟수>
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">신호</td>
      <td style="text-align:left">
        펄스 형태로 출력할 출력신호명<br>
      </td>
      <td style="text-align:left">문자열</td>
    </tr>
    <tr>
      <td style="text-align:left">지연 시간</td>
      <td style="text-align:left">
        프로시져 수행 후 펄스 신호가 시작될 때까지 대기할 시간<br>
        (0.0 ~ 100.0[sec])
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">On 시간</td>
      <td style="text-align:left">
        신호를 On(High) 상태로 출력할 시간<br>
        (0.0 ~ 100.0[sec])
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">Off 시간</td>
      <td style="text-align:left">
        신호를 Off(Low) 상태로 출력할 시간<br>
        (0.0 ~ 100.0[sec])
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">출력 횟수</td>
      <td style="text-align:left">
        펄스 주기를 반복할 횟수
        (0 ~ 1000)
      </td>
      <td style="text-align:left">변수</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
   pulse do10,tlag=0.0,ton=1.5,toff=0.5,cnt=5
   end
```# 6.2 http\_cli 모듈 : HTTP 클라이언트

Hi6 제어기의 범용 이더넷 포트를 통해, 원격의 웹 서비스에 접근하여 HTTP 서비스를 받을 수 있습니다.

이 기능을 사용하기 위해서는 아래와 같이 http\_cli 모듈을 import한 후, HttpCli 객체를 생성해야 합니다.

```python
import http_cli
var cli=http_cli.HttpCli()
```

HttpCli 객체를 생성한 후에는 get, put, post, delete 멤버 프로시져를 호출하여 서비스 요청할 하면 됩니다.

HttpCli 객체는 body라는 이름의 속성을 가지고 있습니다.

get 서비스를 요청하여 성공적으로 응답을 받으면 원격 서버가 응답으로 보내준 데이터는 body 속성이 갖고 있게 됩니다. body 속성 값의 타입은 문자열일 수도 있고, 숫자나 배열, 객체일 수도 있습니다.

put 서비스를 요청할 때는, body 속성에 미리 전송할 데이터를 대입해두어야 합니다.

post 서비스를 요청할 때는 body 속성에 미리 전송할 데이터를 대입해두어야 하며, 원격 서버가 응답으로 보내준 데이터는 body 속성에 보관됩니다.

delete 서비스는 body 속성을 사용하지 않습니다.

제공되는 Http 클라이언트 통신은 동기 통신으로 진행됩니다.


# 6.2.1 생성자

### 설명

HttpCli 객체를 생성합니다. 참조를 리턴합니다.

### 문법

HttpCli\(\)

### 리턴값

생성된 객체의 참조

### 사용 예

```python
var cli = http_cli.HttpCli()
```



# 6.2.2 멤버변수

<table>
  <thead>
    <tr>
      <th style="text-align:left">변수명</th>
      <th style="text-align:left">데이터형</th>
      <th style="text-align:left">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">body</td>
      <td style="text-align:left">모든 형 가능</td>
      <td style="text-align:left">
        <p>put과 post 요청에 실어보낼
          데이터를 미리 넣어두어야
          합니다.
        </p>
        <p>
          body에 object가 아닌 다른 형을 대입시에는 URL의 마지막 경로값을 Key로 처리하여 수행합니다.
        </p>
        <p>get과 post 요청의 응답이 보관됩니다.
          <br/>
        </p>
        <p>HRScript 에서는 직접적으로 body의 멤버변수에 접근을 할 수 없으므로, 해당 내용의 수정, 사용을 위해서는 다른 변수로 대입을 하여 사용 바랍니다.
          <br/>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">query</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">
        <p>
          query를 요구하는 get service에 사용됩니다.
          <br/>
          get 요청에 실어보낼 데이터를 미리 넣어 두어야합니다
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">status</td>
      <td style="text-align:left">int</td>
      <td style="text-align:left">
        <p>
          http 통신 응답 코드와 에러 코드를 반환합니다. (6.2.4 HTTP 통신 코드)
          <br/>
        </p>
      </td>
    </tr>
  </tbody>
</table>

<br/>

body와 query는 object형이 사용됩니다.

object 형은 {key:value}의 형식으로 지원됩니다.

```python
cli.body = { name: "WORK #32", color: "green", state: "OK" }
cli.query = { axis: 3 }
```

# 6.2.3 멤버 프로시져

# get

### 설명

HTTP GET 서비스를 요청합니다.

서버는 요청받은 URL의 정보를 검색하여 응답합니다.

응답 데이터는 body 속성으로 받습니다.

### 문법

&lt;HttpCli객체&gt;.get &lt;URL 문자열, 대기시간, 퇴피주소&gt;


### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>URL 문자열</td>
      <td>
        요청 URL
      </td>
      <td></td>
    </tr>
    <tr>
      <td>대기시간</td>
      <td>
        (Optional) timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행한다.<br>
        지정하지 않으면 무한 대기한다.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        (Optional) timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행한다.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>


### 사용 예

```python
#case 1
var domain="http://192.168.1.200:8888"
cli.get domain+"/setting/max_torque"

#case 2
var url = domain+"/joints/max_speed"
cli.query = {axis: 3}
cli.get(url)
```



# put

### 설명

HTTP PUT 서비스를 요청합니다.

요철된 자원을 수정(update)합니다. 

전송할 데이터는 body 속성에 미리 대입해 두어야 합니다.

### 문법

&lt;HttpCli객체&gt;.put &lt;URL 문자열, 대기시간, 퇴피주소&gt;


### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>URL 문자열</td>
      <td>
        요청 URL
      </td>
      <td></td>
    </tr>
    <tr>
      <td>대기시간</td>
      <td>
        (Optional) timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행한다.<br>
        지정하지 않으면 무한 대기한다.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        (Optional) timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행한다.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
#case 1
var domain="http://192.168.1.200:8888"
cli.body=500
cli.put domain+"/setting/max_torque"

#case 2
var url = domain + "/setting"
cli.body = {max_torque: 500}
cli.put (url, 5000, S1)
```



# post

### 설명

HTTP POST 서비스를 요청합니다.

요청된 자원을 생성(create)합니다.

전송할 데이터는 body 속성에 미리 대입해 두어야 합니다.

응답 데이터는 body 속성으로 받습니다.

### 문법

&lt;HttpCli객체&gt;.post &lt;URL 문자열, 대기시간, 퇴피주소&gt;


### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>URL 문자열</td>
      <td>
        요청 URL
      </td>
      <td></td>
    </tr>
    <tr>
      <td>대기시간</td>
      <td>
        (Optional) timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행한다.<br>
        지정하지 않으면 무한 대기한다.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        (Optional) timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행한다.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
#case 1
var domain="http://192.168.1.200:8888"
cli.body={ name: "WORK #32", color: "green", state: "OK" }
cli.post domain+"/display/update"

#case 2
var url = domain+"/display/update"
cli.post url, 1000, *TimeOut
```

# delete

### 설명

HTTP DELETE 서비스를 요청합니다.

요청한 자원을 삭제합니다.

body 속성은 사용되지 않습니다.

### 문법

&lt;HttpCli객체&gt;.post &lt;URL 문자열, 대기시간, 퇴피주소&gt;


### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>URL 문자열</td>
      <td>
        요청 URL
      </td>
      <td></td>
    </tr>
    <tr>
      <td>대기시간</td>
      <td>
        (Optional) timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행한다.<br>
        지정하지 않으면 무한 대기한다.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        (Optional) timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행한다.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
var domain="http://192.168.1.200:8888"
cli.delete domain+"/items"
```

# 6.2.4 HTTP 통신 코드

* HTTP 주요 응답 코드 
<table>
  <thead>
    <tr>
      <th style="text-align:left">응답대역</th>
      <th style="text-align:left">응답코드</th>
      <th style="text-align:left">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Informational</td>
      <td>
        100
      </td>
      <td>
      continue
      </td>
    </tr>
    <tr>
      <td>
        101
      </td>
      <td>
      Switching protocols
      </td>
    </tr>
    <tr>
    <tr>
      <td rowspan="5">Success</td>
      <td>
        200
      </td>
      <td>
      OK
      </td>
    </tr>
    <tr>
      <td>
        201
      </td>
      <td>
      Created
      </td>
    </tr>
    <tr>
      <td>
        202
      </td>
      <td>
      Accepted
      </td>
    </tr>
    <tr>
      <td>
        203
      </td>
      <td>
      Non-authoritative information
      </td>
    </tr>
    <tr>
      <td>
        204
      </td>
      <td>
      No content
      </td>
    </tr>
    <tr>
    <tr>
      <td rowspan="3">Redirection</td>
      <td>
        301
      </td>
      <td>
      Moved permanently
      </td>
    </tr>
    <tr>
      <td>
        302
      </td>
      <td>
      Not temporarily
      </td>
    </tr>
    <tr>
      <td>
        303
      </td>
      <td>
      Not modified
      </td>
    </tr>
    <tr>
      <td rowspan="11">Client error</td>
      <td>
        400
      </td>
      <td>
      Bad Request
      </td>
    </tr>
    <tr>
      <td>
        401
      </td>
      <td>
      Unauthorized 
      </td>
    </tr>
    <tr>
      <td>
        402
      </td>
      <td>
      Payment required
      </td>
    </tr>
    <tr>
      <td>
        403
      </td>
      <td>
      Forbidden 
      </td>
    </tr>
    <tr>
      <td>
        404
      </td>
      <td>
      Not found 
      </td>
    </tr>
    <tr>
      <td>
        405
      </td>
      <td>
      Method not allowed
      </td>
    </tr>
    <tr>
      <td>
        407
      </td>
      <td>
      Proxy authentication required 
      </td>
    </tr>
    <tr>
      <td>
        408
      </td>
      <td>
      Request timeout
      </td>
    </tr>
    <tr>
      <td>
        410
      </td>
      <td>
      Gone  
      </td>
    </tr>
    <tr>
      <td>
        412
      </td>
      <td>
      Precondition failed
      </td>
    </tr>
    <tr>
      <td>
        414
      </td>
      <td>
      Request-URI too long
      </td>
    </tr>
    <tr>
      <td rowspan="5">Server error</td>
      <td>
        500
      </td>
      <td>
       Internal server error 
      </td>
    </tr>
    <tr>
      <td>
        501
      </td>
      <td>
      Not implemented
      </td>
    </tr>
    <tr>
      <td>
        503
      </td>
      <td>
      Service unnailable
      </td>
    </tr>
    <tr>
      <td>
        504
      </td>
      <td>
      Gateway timeout
      </td>
    </tr>
    <tr>
      <td>
        505
      </td>
      <td>
      HTTP version not supported
      </td>
    </tr>
  </tbody>
</table>


* 에러 코드(Exception)

<table>
  <thead>
    <tr>
    <th style="text-align:left">에러명</th>
      <th style="text-align:left">에러코드</th>
      <th style="text-align:left">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>RequestException</td>      
      <td>
        -1
      </td>
      <td>
      There was an ambiguous exception that occurred while handling your request.
      </td>
    </tr>
    <tr>
      <td> ConnectionErr</td>
      <td>
        -2
      </td>
      <td>
      In the event of a network problem (e.g. DNS failure, refused connection, etc)
      </td>
    </tr>
    <tr>
    <td> HTTPError
      <td>
        -3
      </td>
      <td>
      It will occur if the HTTP request returned an unsuccessful status code.
      </td>
    </tr>
    <tr>
    <td>URLRequired</td>
      <td>
        -4
      </td>
      <td>
      A valid URL is required to make a request.
      </td>
    </tr>
    <tr>
    <td>TooManyRedirects</td>
      <td>-5</td>
      <td>
      If a request exceeds the configured number of maximum redirections, a TooManyRedirects exception is raised.
      </td>
    </tr>
    <tr>
    <td>Timeout</td>
      <td>
        -6
      </td>
      <td>
      If a request times out, a Timeout exception is raised.
      </td>
    </tr>
  </tbody>
</table>
    
  # 6.2.4 HTTP client 통신 예제

```python
     import http_cli
     var cli=http_cli.HttpClient()
     var url, body, query, status_code
     var domain="http://192.168.1.200:8888"

     # get
     cli.get domain+"/device/direction"
     body = cli.body

     #check the communication status
     if cli.status>=400 or cli.status<0
        goto 99 		#http communication error
     endif

     # put
     url = domain+"/device/direction"
     body.ry=90
     cli.body=body
     cli.put(url, 3000, *Timeout)

     # post
     cli.body={ name: "WORK #32", color: "green", state: "OK" }
     cli.post domain+"/display/update", 5000, *Timeout

     # delete
     cli.delete(domain+"/items")

     end
     
  99 print "error status"
     
     *Timeout
     print "timeout"
```

# 6.3 티치펜던트 console bar로 입출력하기

# 6.3.1 print문

### 설명

print문을 통해 티치펜던트의 안내표시줄에 문자열을 출력합니다. 문자열 상수 뿐만 아니라, 어떤 타입의 표현식(상수, 변수 포함)을 지정해도 그 결과를 문자열로 변환하여 출력합니다. 표현식을 여러 개 지정하면 각 표현식들을 공백 1글자로 구분하여 출력합니다.

### 문법

```python
print <표현식>[,<표현식>,<표현식>...]
```


### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">표현식 (expression)</td>
      <td style="text-align:left">
        출력할 표현식. 논리, 숫자, 문자열, 배열, 객체의 모든 타입을 지원합니다.
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
print "hello, world"
print arr[0],arr[1],arr[2]
print "x-center: "+(width/2), "y-center: "+(height/2)
print po10+sft21
```
# 6.3.2 input문

### 설명

input문을 통해 티치펜던트의 키입력으로 문자열을 입력받아 변수에 저장합니다. 제한시간까지 입력되지 않으면 다음 명령문으로 진행하거나 timeout 주소로 분기합니다.

### 문법

input &lt;변수&gt;\[,&lt;제한시간&gt;,&lt;timeout 주소&gt;\]



### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">변수</td>
      <td style="text-align:left">
        <p>입력을 받을 변수. 숫자도
          문자열 타입으로 입력받습니다.
          수치값이 필요하면 int(
          )나 double( ) 함수로 변환하십시오.
          <br
          />
        </p>
        <p>
          <br />
        </p>
        <p>
          <br />
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">제한시간</td>
      <td style="text-align:left">입력을 대기할 최대 제한
        시간 (timeout)</td>
      <td style="text-align:left">
        <p>산술식
          <br />
        </p>
        <p>0.1~60.0 sec
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">timeout 주소</td>
      <td style="text-align:left">제한시간 초과 시, 분기할
        주소</td>
      <td style="text-align:left">주소</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
input work_no
input work_no,10
input work_no,10,*timeout
```

![](../../_assets/image_6.png)



# 6.4 modbus 모듈 : 모드버스 마스터

HRScript에서 모드버스 마스터 동작을 수행할 수 있습니다. 모드버스 통신 기능에 대한 자세한 내용은 별도의 [Hi6 로봇제어기 기능설명서 - 모드버스](https://hrbook-hrc.web.app/#/view/doc-modbus/korean/README)를 참조하십시오.  
# 6.5 sci 모듈 : 시리얼 통신

Hi6 제어기의 COM 포트를 통해, 시리얼 통신을 수행할 수 있습니다.

이 기능을 사용하기 위해서는 아래와 같이 sci 모듈을 import한 후, Sci 객체를 생성해야 합니다.

또한 사용하기 전에 반드시 [시스템 > 2. 제어파라미터 > 3. 시리얼 포트] 의 설정 사양을 확인하세요.

```python
import sci
var sci2=sci.Sci(2)
```

Sci 객체를 생성한 후에는 send, recv, open, close 멤버 프로시져를 호출하면 됩니다.

send를 호출할 때는, 미리 전송할 문자열을 대입해두어야합니다.

recv를 호출할 때는, 성공적으로 수신하면 응답 문자열을 반환합니다. 

open를 호출하여 port를 open 하게 됩니다. 

close를 호출하여 port를 close 하게 됩니다.



# 6.5.1 생성자

### 설명

Sci 객체를 생성합니다. 참조를 리턴합니다.

### 문법

Sci(port number)

### 리턴값

생성된 객체의 참조

### 사용 예

```python
var sci2 = sci.Sci(2)
```



# 6.5.2 멤버 프로시져# send

### 설명

Sci의 send 를 호출하여 문자열을 송신합니다.

### 문법

&lt;Sci객체&gt;.send(송신 문자열)

### 리턴값

송신 문자열의 길이

### 사용 예

```python
sci2.send("test")
or
sci2.send "test"
```



# recv

### 설명

Sci의 recv 를 호출하여 문자열을 수신합니다.


### 문법

&lt;Sci객체&gt;.recv \[{대기시간}\] \[, {퇴피주소}\]


### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>대기시간</td>
      <td>
        timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행한다.<br>
        지정하지 않으면 무한 대기한다.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행한다.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>

### 리턴값

수신한 문자열

### 사용 예

```python
   var msg = sci2.recv(5000, 99)
99 print "error"
```



# open

### 설명

Sci의 open 를 호출하여 시리얼 포트를 오픈합니다.

제어기 설정을 통해 기 설정된 내용으로 시리얼 포트를 오픈하게 되며, 이전에 해당 포트를 close한 경우 외 에는 open을 별도로 수행 할 필요가 없습니다.(기본값: open)


### 문법

&lt;Sci객체&gt;.open

### 리턴값
- 0: 오픈 성공
- <0: 오픈 실패


### 사용 예

```python
sci2.open
```



# close

### 설명

Sci의 close 를 호출하여 시리얼 포트를 닫습니다.


### 문법

&lt;Sci객체&gt;.close

### 리턴값
- 0: 닫기 성공
- -1: 이미 닫혔음.

### 사용 예

```python
sci2.close
```



# 6.5.3 시리얼 통신 예제

``` python
Hyundai Robot Job File; { version: 1.6, mech_type: "388(HS220-02)", total_axis: 6, aux_axis: 0 }
     
     # sci 모듈 import 후, 생성자로 Sci 객체 생성 
     import sci
     var sci2=sci.Sci(2)   #port no. (com2)
     
     # default open
     # send
     sci2.send "test"

     # receive (선택옵션: 3000msec 타임 아웃시, 99행으로 분기)
     var msg=sci2.recv(3000,99)
     print msg

     # close 
     sci2.close
     
     # re-open
     sci2.open

     end

  99 print "error"

```


# 7 enet 모듈 : 이더넷 TCP/UDP 통신

Hi6 제어기의 범용 이더넷 포트를 통해, 외부 장치와 이더넷 TCP 혹은 UDP 통신으로 문자열, 혹은 바이너리 데이터의 송수신을 할 수 있습니다.

enet 모듈은 ENet과 BBuf의 2개의 객체를 생성할 수 있습니다. ENet은 이더넷 socket 인터페이스를 제공하고, BBuf는 바이너리 데이터 통신을 할 때 사용됩니다.  

client 예제와 server 예제를 따라가면서 사용법을 이해해 봅시다. 각 객체의 멤버 변수와 함수들의 참조설명서(reference guide)는 그 뒤에 이어집니다.
# 7.1 peer-to-peer, client 예제

UDP peer-to-peer (1:1통신), 혹은 TCP client 예제 프로그램을 문자열과 바이너리 송수신 방식으로 나누어 설명합니다.
# 7.1.1 peer-to-peer, client 예제 - 문자열 송수신

다음과 같은 순서로 수행합니다.

1. `enet` 모듈 import 후, 생성자로 `ENet` 객체 생성.
2. 멤버변수로 IP주소와 port번호를 설정.
3. `open` 멤버 프로시져로 ethernet socket 열고, `state()` 멤버변수로 상태 확인.  
\(TCP통신인 경우에는 `open` 후 `connect` 프로시져도 수행해야 함.\)
4. `send`, `recv` 멤버 프로시져로 송수신 수행.
5. `close` 멤버 프로시져로 통신 연결 닫기.

<br>

### UDP peer-to-peer
```python
     # 1. enet 모듈 import 후, 생성자로 ENet 객체 생성
     import enet
     var cli=enet.ENet() # TCP 통신인 경우, ENet("tcp")

     # 2. IP주소와 port번호 설정
     cli.ip_addr="192.168.1.172" # remote (상대방) IP address
     cli.lport=51001 # local (자신) port
     cli.rport=51002 # remote (상대방) port 
     # (port no. 49152–65535 contains dynamic or private ports)

     # 3. ethernet socket 열기
     cli.open

     print cli.state() # 1이면 정상

     # --------------------------------
     # 4-1. string 송신
     cli.send "hello, peer.\n"

     # 4-2. string 수신
     #     (5초간 수신 없으면 *TimeOut 레이블로 jump)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # 수신된 문자열
     print msg
     delay 1.0
     # --------------------------------

     # 5. ethernet socket 닫기
     cli.close
     print cli.state() # 0이면 정상
     delay 1.5
     end

     *TimeOut
     print "time out!"
     cli.close
     end
```
<br>

### TCP client
(peer-to-peer와는 `lport`와 `connect` 부분만 다름.)
```python
     # 1. enet 모듈 import 후, 생성자로 ENet 객체 생성
     import enet
     var cli=enet.ENet() # TCP 통신인 경우, ENet("tcp")

     # 2. IP주소와 port번호 설정
     cli.ip_addr="192.168.1.172" # remote (상대방) IP address
     cli.lport=0 # local (자신) port; 무작위
     cli.rport=51002 # remote (상대방) port 
     # (port no. 49152–65535 contains dynamic or private ports)

     # 3. ethernet socket 열기
     cli.open
     cli.connect # 서버에 접속.
     print cli.state() # 1이면 정상

     # --------------------------------
     # 4-1. string 송신
     cli.send "hello, peer.\n"

     # 4-2. string 수신
     #     (5초간 수신 없으면 *TimeOut 레이블로 jump)
     var msg
     cli.recv 5000, *TimeOut
     var msg=result() # 수신된 문자열
     print msg
     delay 1.0
     # --------------------------------

     # 5. ethernet socket 닫기
     cli.close
     print cli.state() # 0이면 정상
     delay 1.5
     end

     *TimeOut
     print "time out!"
     cli.close
     end
```# 7.1.2 peer-to-peer, client 예제 - 바이너리 송수신

바이너리 송수신은 `BBuf` (Binary Buffer) 객체를 통해 수행합니다.  
(송수신 부분만 다르고, 나머지는 문자열 송수신과 동일합니다.)

송신

1. `enet.BBuf` 객체 생성.
2. 원하는 바이너리 데이터를 `BBuf.append()` 함수로 `BBuf` 객체에 추가.
3. `ENet.send_bbuf()` 함수로 BBuf 객체를 송신.


수신

1. `enet.BBuf` 객체 생성.
2. `ENet.recv_bbuf()` 함수로 BBuf 객체에 바이너리 데이터를 수신
3. 원하는 바이너리 데이터를 `BBuf.read_nums()` 함수로 `BBuf` 객체로부터 읽기.


<br>

### UDP peer-to-peer
```python
     # 1. enet 모듈 import 후, 생성자로 ENet 객체 생성
     import enet
     var cli=enet.ENet() # TCP 통신인 경우, ENet("tcp")

     # 2. IP주소와 port번호 설정
     cli.ip_addr="192.168.1.172" # remote (상대방) IP address
     cli.lport=51001 # local (자신) port
     cli.rport=51002 # remote (상대방) port 
     # (port no. 49152–65535 contains dynamic or private ports)

     # 3. ethernet socket 열기
     cli.open
     
     print cli.state() # 1이면 정상

     # 송신 --------------------------------
     # 4-1. BBuf 객체 생성
     var bbuf=enet.BBuf()

     # (sample binary data)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. binary data를 BBuf 객체에 추가.
     bbuf.clear()
     bbuf.append("s4", arr) # little endian signed-4byte data 추가

     # 4-3. BBuf 객체를 송신
     var ret
     ret=cli.send_bbuf(bbuf)

     # 수신 --------------------------------
     # 4-1. BBuf 객체 생성
     var bbuf2=enet.BBuf()
     
     # 4-2. BBuf 객체에 binary data를 수신
     #     (3초간 수신 없으면 *TimeOut 레이블로 jump)
     cli.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. binary data를 BBuf 객체로부터 읽기.
     var nums=bbuf2.read_nums("U2", 0, 3) # big-endian unsigned-2byte data 3개 읽기
     print nums
     # --------------------------------

     # 5. ethernet socket 닫기
     cli.close
     print cli.state() # 0이면 정상
     delay 1.5
     end

     *TimeOut
     print "time out!"
     cli.close
     end
```

### TCP client
(peer-to-peer와는 `lport`와 `connect` 부분만 다름.)
```python
     # 1. enet 모듈 import 후, 생성자로 ENet 객체 생성
     import enet
     var cli=enet.ENet() # TCP 통신인 경우, ENet("tcp")

     # 2. IP주소와 port번호 설정
     cli.ip_addr="192.168.1.172" # remote (상대방) IP address
     cli.lport=0 # local (자신) port; 무작위
     cli.rport=51002 # remote (상대방) port 
     # (port no. 49152–65535 contains dynamic or private ports)

     # 3. ethernet socket 열기
     cli.open
     cli.connect # 서버에 접속.
     print cli.state() # 1이면 정상

     # 송신 --------------------------------
     # 4-1. BBuf 객체 생성
     var bbuf=enet.BBuf()

     # (sample binary data)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. binary data를 BBuf 객체에 추가.
     bbuf.clear()
     bbuf.append("s4", arr) # little endian signed-4byte data 추가

     # 4-3. BBuf 객체를 송신
     var ret
     ret=cli.send_bbuf(bbuf)

     # 수신 --------------------------------
     # 4-1. BBuf 객체 생성
     var bbuf2=enet.BBuf()
     
     # 4-2. BBuf 객체에 binary data를 수신
     #     (3초간 수신 없으면 *TimeOut 레이블로 jump)
     cli.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. binary data를 BBuf 객체로부터 읽기.
     var nums=bbuf2.read_nums("U2", 0, 3) # big-endian unsigned-2byte data 3개 읽기
     print nums
     # --------------------------------

     # 5. ethernet socket 닫기
     cli.close
     print cli.state() # 0이면 정상
     delay 1.5
     end

     *TimeOut
     print "time out!"
     cli.close
     end
```


* "s4"나 "U2" 같은 문자열 인수가 endian 방식, signed/unsigned, byte수 같은 binary data 형식을 결정합니다. 자세한 내용은 [7.4.2 지원 형식 (format)](../4-bbuf/2-format.md)을 참조하십시오.# 7.2 TCP server 예제

TCP server 예제 프로그램을 문자열과 바이너리 송수신 방식으로 나누어 설명합니다.

TCP client가 `connect()` 함수로 server에 접속하는 반면, TCP server는 `listen()` 함수를 수행한 후, `accept()` 함수로 client의 connect를 기다립니다.  

* 동시에 1개의 client 접속만 허용합니다.
* remote port는 지정할 필요 없습니다.

나머지 동작들은 client와 동일합니다.
# 7.2.1 ethernet TCP server 예제 - 문자열 송수신

다음과 같은 순서로 수행합니다.

1. `enet` 모듈 import 후, 생성자로 ENet 객체 생성.
2. 멤버변수로 IP주소와 port번호를 설정. (remote port 설정은 필요없음.)
3. `open` 멤버 프로시져로 ethernet socket 열고, `listen()`, `accept()` 함수를 수행함. `state()` 멤버변수로 상태 확인.
4. `send`, `recv` 멤버 프로시져로 송수신 수행.
5. `close` 멤버 프로시져로 통신 연결 닫기.


```python
     # 1. enet 모듈 import 후, 생성자로 ENet 객체 생성
     import enet
     var svr=enet.ENet("tcp")
     
     # 2. IP주소와 port번호 설정
     svr.ip_addr="192.168.1.172" # remote (상대방) IP address
     svr.lport=51001 # local (자신) port
     # (port no. 49152–65535 contains dynamic or private ports)
     
     # 3. ethernet socket 열기
     svr.open
     var ret
     ret=svr.listen()
     ret=svr.accept() # client로부터의 connect 대기
     print svr.state() # 1이면 정상
     
     # --------------------------------
     # 4-1. string 송신
     svr.send "Welcome, I am a TCP server.\n"
     
     # 4-2. string 수신
     #     (5초간 수신 없으면 *TimeOut 레이블로 jump)
     svr.recv 5000,*TimeOut
     var msg=result() # 수신된 문자열
     print msg
     delay 1.0
     # --------------------------------
     
     # 5. ethernet socket 닫기
     svr.close
     print svr.state() # 0이면 정상
     delay 1.5
     end

     *TimeOut
     print "time out!"
     svr.close
     end
```
# 7.2.2 ethernet TCP server 예제 - 바이너리 송수신

바이너리 송수신은 BBuf (Binary Buffer) 객체를 통해 수행합니다.  
(송수신 부분만 다르고, 나머지는 문자열 송수신과 동일합니다.)

송신

1. `enet.BBuf` 객체 생성.
2. 원하는 바이너리 데이터를 `BBuf.append()` 함수로 `BBuf` 객체에 추가.
3. `ENet.send_bbuf()` 함수로 BBuf 객체를 송신.


수신

1. `enet.BBuf` 객체 생성.
2. `ENet.recv_bbuf()` 함수로 `BBuf` 객체에 바이너리 데이터를 수신
3. 원하는 바이너리 데이터를 `BBuf.read_nums()` 함수로 `BBuf` 객체로부터 읽기.


```python
     # 1. enet 모듈 import 후, 생성자로 ENet 객체 생성
     import enet
     var svr=enet.ENet("tcp")
     
     # 2. IP주소와 port번호 설정
     svr.ip_addr="192.168.1.172" # remote (상대방) IP address
     svr.lport=51001 # local (자신) port
     # (port no. 49152–65535 contains dynamic or private ports)
     
     # 3. ethernet socket 열기
     svr.open
     var ret
     ret=svr.listen()
     ret=svr.accept() # client로부터의 connect 대기
     print svr.state() # 1이면 정상

     # 송신 --------------------------------
     # 4-1. BBuf 객체 생성
     var bbuf=enet.BBuf()

     # (sample binary data)
     var arr=[ -3, 0, 1 ]
     
     # 4-2. binary data를 BBuf 객체에 추가.
     bbuf.clear()
     bbuf.append("s4", arr) # little endian signed-4byte data 추가

     # 4-3. BBuf 객체를 송신
     ret=svr.send_bbuf(bbuf)

     # 수신 --------------------------------
     # 4-1. BBuf 객체 생성
     var bbuf2=enet.BBuf()
     
     # 4-2. BBuf 객체에 binary data를 수신
     #     (3초간 수신 없으면 *TimeOut 레이블로 jump)
     svr.recv_bbuf bbuf2,3000,*TimeOut

     # 4-3. binary data를 BBuf 객체로부터 읽기.
     var nums=bbuf2.read_nums("U2", 0, 3) # big-endian unsigned-2byte data 3개 읽기
     print nums
     # --------------------------------

     # 5. ethernet socket 닫기
     svr.close
     print svr.state() # 0이면 정상
     delay 1.5
     end

     *TimeOut
     print "time out!"
     svr.close
     end
```

* "s4"나 "U2" 같은 문자열 인수가 endian 방식, signed/unsigned, byte수 같은 binary data 형식을 결정합니다. 자세한 내용은 [7.4.2 지원 형식 (format)](../4-bbuf/2-format.md)을 참조하십시오.
# 7.3 ENet 객체

`ENet` 객체는 이더넷 통신을 위한 socket 인터페이스를 제공합니다.  
사용법은 앞 절의 예제를 참고하십시오.
# 7.3.1 ENet 생성자

### 설명

이더넷 객체를 생성합니다. 생성된 객체의 참조를 리턴합니다.

### 문법

`ENet({프로토콜})`

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>프로토콜</td>
      <td>
        "tcp" : TCP 통신<br>
        "udp" : UDP 통신<br>
        생략하면 "udp"로 인식</td>
    </tr>
  </tbody>
</table>

### 리턴값

생성된 객체의 참조

### 사용 예

```python
enet0 = ENet()
var tcp = ENet("tcp")
```
# 7.3.2 ENet 멤버변수

<table>
  <thead>
    <tr>
      <th style="text-align:left">변수명</th>
      <th style="text-align:left">데이터형</th>
      <th style="text-align:left">설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ip_addr</td>
      <td style="text-align:left">문자열</td>
      <td style="text-align:left">
        읽기/쓰기 가능.<br>
        통신상대의 IP 주소를 지정하거나 얻습니다.<br>
        open문 호출 시에만 적용됩니다.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rport</td>
      <td style="text-align:left">숫자</td>
      <td style="text-align:left">
        읽기/쓰기 가능.<br>
        통신상대(Remote)의 포트번호를 지정하거나 얻습니다.<br>
        open문 호출 시에만 적용됩니다.
      </td>
    </tr>
    <tr>
      <td style="text-align:left">lport</td>
      <td style="text-align:left">숫자</td>
      <td style="text-align:left">
        읽기/쓰기 가능.<br>
        UDP peer-to-peer 통신과 TCP server에서만 사용되며, TCP client에서는 무시됩니다.<br>
        제어기 자신의(Local)의 포트번호를 지정하거나 얻습니다.<br>
        디폴트 값은 0이며(지정하지 않은 경우), 이 경우에는 자신의 포트번호는 자동 생성됩니다.<br>
        open문 호출 시에만 적용됩니다.
      </td>
    </tr>
  </tbody>
</table>

# 7.3.3 ENet 멤버 함수

* 멤버 함수는 리턴값을 받을 때는 반드시 인수를 괄호로 묶어주십시오.  
  
  ```python
  var nitem=obj.func(param1,param2) # (O) ; 괄호 필수
  var nitem=obj.func param1,param2 # (X) ; 문법 오류
  ```

* 리턴값을 받지 않을 때는 괄호를 생략할 수 있습니다.  

  ```python
  obj.func(param1,param2) # (O)
  obj.func param1,param2 # (O) ; 괄호 생략
  ```# accept

### 설명

이더넷 TCP 통신에서 server로서 client측의 연결 요청이 올 때까지 기다립니다. 요청이 발생하면 연결을 만듭니다.  
UDP peer-to-peer 통신에서는 사용되지 않습니다.

### 문법

`{ENet객체}.accept [{대기시간}][,{퇴피주소}]`

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>대기시간</td>
      <td>
        timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행.<br>
        지정하지 않으면 무한 대기.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>


### 리턴값

<table>
  <thead>
    <tr>
      <th style="text-align:left">값</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>
        성공 (완료)
      </td>
      <td></td>
    </tr>  
    <tr>
      <td>0</td>
      <td>
        대기 중
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>timeout</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>error</td>
      <td></td>
    </tr>    
  </tbody>
</table>


### 사용 예

```python
enet_to_sensor.listen
var ret=enet_to_sensor.accept(5000)
```

```python
enet_to_sensor.listen
enet_to_sensor.accept 5000,*TimeOut
```

# close

### 설명

이더넷 TCP 혹은 UDP 통신을 위한 연결을 닫습니다.

### 문법

`{ENet객체}.close`

### 사용 예

```python
enet_to_sensor.close
```

# connect

### 설명

이더넷 TCP 통신에서 client로서 server에 연결을 시도합니다.  
UDP peer-to-peer 통신에서는 사용되지 않습니다.

### 문법

`{ENet객체}.connect [{대기시간}] [, {퇴피주소}]`


### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>대기시간</td>
      <td>
        timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행.<br>
        지정하지 않으면 무한 대기.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>


### 리턴값

<table>
  <thead>
    <tr>
      <th style="text-align:left">값</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>
        성공
      </td>
      <td></td>
    </tr>  
    <tr>
      <td>0</td>
      <td>
        대기 중
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>timeout</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>error</td>
      <td></td>
    </tr>
  </tbody>
</table>


### 사용 예

```python
var ret=enet_to_sensor.connect(5000)
```

```python
enet_to_sensor.connect 5000,*TimeOut
```# listen

### 설명

이더넷 TCP 통신에서 server로서 client의 연결을 준비합니다.  
UDP peer-to-peer 통신에서는 사용되지 않습니다.

### 문법

`{ENet객체}.listen [{backlog}]`

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>backlog</td>
      <td>
        accept 되지 않은 연결의 허용 개수<br>
        지정하지 않으면 적절한 값이 선택됩니다.
      </td>
      <td></td>
    </tr>
  </tbody>
</table>


### 리턴값

<table>
  <thead>
    <tr>
      <th style="text-align:left">값</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>
        성공
      </td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>에러</td>
      <td></td>
    </tr>	 
  </tbody>
</table>


### 사용 예

```python
enet_to_sensor.listen
enet_to_sensor.accept 5000,*TimeOut
```
# open

### 설명

이더넷 TCP 혹은 UDP 통신을 위한 연결을 엽니다.

### 문법

`{ENet객체}.open`

### 사용 예

```python
enet_to_sensor.open
```

# recv

### 설명

이더넷 객체로 문자열을 수신합니다. 수신된 문자열은 리턴값이나 `result()` 함수로 얻을 수 있습니다.

### 문법

`{ENet객체}.recv [{대기시간}][,{퇴피주소}]`



### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>대기시간</td>
      <td>
        timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행.<br>
        지정하지 않으면 무한 대기.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>

### 리턴값

수신한 문자열

### 사용 예

```python
var msg
msg=enet_to_sensor.recv
msg=enet_to_sensor.recv(5000)
msg=enet_to_sensor.recv(5000,*TimeOut)
end

*TimeOut
print "Time out! No response from sensor"
end
```
# recv_bbuf

### 설명

이더넷 객체로부터 바이너리 데이터를 수신하여 [BBuf](../../4-bbuf/README.md) 객체에 저장합니다.

### 문법

`{ENet객체}.recv_bbuf {BBuf객체}[,{대기시간}][,{퇴피주소}]`



### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>BBuf객체</td>
      <td>
        수신한 바이너리 데이터를 저장 할 BBuf객체
      </td>
      <td></td>
    </tr>
    <tr>
      <td>대기시간</td>
      <td>
        timeout 시간. 경과하면 다음 명령문, 혹은 퇴피스텝으로 진행한다.<br>
        지정하지 않으면 무한 대기한다.
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>퇴피주소</td>
      <td>
        timeout 일 때 분기할 주소.<br>
        지정하지 않으면 다음 주소로 진행한다.
      </td>
      <td>주소</td>
    </tr>
  </tbody>
</table>

### 리턴값

수신한 데이터 개수

### 사용 예

```python
var bbuf=enet_to_sensor.BBuf()
enet_to_sensor.recv bbuf
enet_to_sensor.recv bbuf, 5000
var nitem=enet_to_sensor.recv(bbuf,5000,*TimeOut)
end

*TimeOut
print "Time out! No response from sensor"
end
```

# send

### 설명

이더넷 객체로 문자열을 송신합니다.

### 문법

`{ENet객체}.send {msg}`



### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">msg</td>
      <td style="text-align:left">
        송신할 문자열.
      </td>
      <td style="text-align:left">문자열형</td>
    </tr>
  </tbody>
</table>


### 리턴값

송신한 바이트 수


### 사용 예

```python
enet_to_sensor.send "rob:" + 10 + ", command:"+cmd, "\n"
```



# send_bbuf

### 설명

이더넷 객체로 [BBuf](../../4-bbuf/README.md) 객체를 송신합니다.

### 문법

`{ENet객체}.send_bbuf {BBuf객체}`



### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">BBuf객체</td>
      <td style="text-align:left">
        송신할 Binary Buffer 객체.
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>


### 리턴값

송신한 바이트 수


### 사용 예

```python
var bbuf=enet.BBuf()
var arr=[ -3, 0, 1 ]
bbuf.append("s4", arr)
var nitem=cli.send_bbuf(bbuf)
```



# set_send_trail_null

### 설명

`ENet.send()` 함수로 문자열을 송신할 때, 종료 null문자(terminating-null)를 붙여서 송신할 지 여부를 설정합니다. (default는 false)

### 문법

`{ENet객체}.set_send_trail_null(true|false)`


### 리턴값

없음.


### 사용 예

```python
enet_to_sensor.set_send_trail_null(true)
enet_to_sensor.send "ACK"
enet_to_sensor.set_send_trail_null(false)
```
# state

### 설명

이더넷 객체의 상태를 리턴합니다.

### 문법

`{ENet객체}.state`



### 리턴값

<table>
  <thead>
    <tr>
      <th style="text-align:left">값</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>
        연결됨. <br>
        (UDP일 때는 `open`만 해도 연결로 간주됩니다.<br>
        TCP일 때는 `open` 후 `listen`, `connect`, `accept`도 수행되어야 연결로 간주됩니다.)
      </td>
      <td></td>
    </tr>
    <tr>
      <td>0</td>
      <td>연결 안됨.</td>
      <td></td>
    </tr>
    <tr>
      <td>-1</td>
      <td>이더넷소켓 생성 실패</td>
      <td></td>
    </tr>
    <tr>
      <td>-2</td>
      <td>이더넷장치 BIND 실패</td>
      <td></td>
    </tr>
    <tr>
      <td>-3</td>
      <td>connect 실패</td>
      <td></td>
    </tr>
    <tr>
      <td>-4</td>
      <td>listen 실패</td>
      <td></td>
    </tr>
    <tr>
      <td>-5</td>
      <td>accept 실패</td>
      <td></td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
var ret = enet_to_sensor.state()
```

# 7.4 BBuf 객체

BBuf (Binary Buffer) 객체는 이더넷 통신으로 송수신할 바이너리 데이터를 캡슐화합니다. 
사용법은 바이너리 통신 예제를 참고하십시오.

[7.1.2 peer-to-peer, client 예제 - 바이너리 송수신](../1-exam-client/2-enet-client-bin.md)

[7.2.2 ethernet TCP server - 바이너리 송수신](../2-exam-server/2-enet-server-bin.md)
# 7.4.1 BBuf 생성자

### 설명

바이너리 버퍼(Binary Buffer) 객체를 생성합니다. 생성된 객체의 참조를 리턴합니다.

### 문법

`BBuf()`


### 리턴값

생성된 객체의 참조

### 사용 예

```python
var bbuf = BBuf()
```


# 7.4.2 지원 형식 (format)

멤버함수인 `append()`나 `read_num()`는 인수로 형식을 지정해야 합니다.  

형식은 Signed/Unsigned/Floating-point 를 의미하는 영문자 1개와 byte 수를 의미하는 숫자 1개로 구성됩니다.<br>
영문자가 대문자이면 big endian, 소문자이면 little endian입니다.			



<table>
  <thead>
    <tr>
      <th>형식</th>
      <th>endian</th>
      <th>타입</th>
      <th>바이트수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>"S1"</td>
      <td>big endian<br>
      <td>부호있는 정수 (signed integer)<br>
      <td>1byte<br>
    </tr>
    <tr>
      <td>"S2"</td>
      <td>big endian<br>
      <td>부호있는 정수 (signed integer)<br>
      <td>2byte<br>
    </tr>
    <tr>
      <td>"S4"</td>
      <td>big endian<br>
      <td>부호있는 정수 (signed integer)<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"U1"</td>
      <td>big endian<br>
      <td>부호없는 정수 (unsigned integer)<br>
      <td>1byte<br>
    </tr>
    <tr>
      <td>"U2"</td>
      <td>big endian<br>
      <td>부호없는 정수 (unsigned integer)<br>
      <td>2byte<br>
    </tr>
    <tr>
      <td>"U4"</td>
      <td>big endian<br>
      <td>부호없는 정수 (unsigned integer)<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"F4"</td>
      <td>big endian<br>
      <td>단정도 실수 (single-precision real)<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"F8"</td>
      <td>big endian<br>
      <td>배정도 실수 (double-precision real)<br>
      <td>8byte<br>
    </tr>
    <tr>
      <td>"s1"</td>
      <td>little endian<br>
      <td>부호있는 정수 (signed integer)<br>
      <td>1byte<br>
    </tr>
    <tr>
      <td>"s2"</td>
      <td>little endian<br>
      <td>부호있는 정수 (signed integer)<br>
      <td>2byte<br>
    </tr>
    <tr>
      <td>"s4"</td>
      <td>little endian<br>
      <td>부호있는 정수 (signed integer)<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"u1"</td>
      <td>little endian<br>
      <td>부호없는 정수 (unsigned integer)<br>
      <td>1byte<br>
    </tr>
    <tr>
      <td>"u2"</td>
      <td>little endian<br>
      <td>부호없는 정수 (unsigned integer)<br>
      <td>2byte<br>
    </tr>
    <tr>
      <td>"u4"</td>
      <td>little endian<br>
      <td>부호없는 정수 (unsigned integer)<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"f4"</td>
      <td>little endian<br>
      <td>단정도 실수 (single-precision real)<br>
      <td>4byte<br>
    </tr>
    <tr>
      <td>"f8"</td>
      <td>little endian<br>
      <td>배정도 실수 (double-precision real)<br>
      <td>8byte<br>
    </tr>
	 <tr>

  </tbody>
</table># 7.4.2 BBuf 멤버 함수

# append

### 설명

바이너리 버퍼에 지정된 형식(format)으로 데이터를 추가합니다.


### 문법

`{BBuf객체}.append {format},{data}`


### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">format</td>
      <td style="text-align:left">
			바이너리 데이터 형식(format)<sup>*</sup><br>
      e.g. "U4", "s2"
      </td>
      <td style="text-align:left">문자열형</td>
    </tr>
	 <tr>
      <td style="text-align:left">data</td>
      <td style="text-align:left">
        바이너리 버퍼에 추가할 데이터
      </td>
      <td style="text-align:left">기본형(primitive) 데이터,<br>혹은 기본형 데이터의 1차원 배열</td>
    </tr>
  </tbody>
</table>

<br>


\* [7.4.2 지원 형식 (format)](../2-format.md)을 참조하십시오.  

* format과 다른 type의 data를 지정하면 암시적으로 자동 형변환이 수행됩니다. 가령, format이 "s2"(2byte 정수)인데, data가 3.7이라는 float 값이었다면, buffer에는 정수값 3(0x0003)이 append 됩니다.
반대로, format이 "f4"(4byte 실수)인데, data가 -3이라는 정수값이면, buffer에는 실수값 -3.0(0xC0400000)이 저장됩니다.  
* format이 unsigned인데 data가 음수이면 에러가 발생하므로 주의하십시오.
<br>
<br>


### 리턴값

추가된 데이터의 개수


### 사용 예

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
```
# clear

### 설명

바이너리 버퍼에 저장된 데이터를 전부 삭제합니다.


### 문법

`{BBuf객체}.clear()`


### 리턴값

없음


### 사용 예

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
bbuf.clear()
```
# nbyte

### 문법

`{BBuf객체}.nbyte`


### 리턴값

바이너리 데이터의 크기 (byte수)


### 사용 예

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
print bbuf.nbyte() # "8"
```

# read_num

### 설명

바이너리 버퍼의 지정 위치로부터 숫자형 값을 읽어 리턴합니다.


### 문법

`{BBuf객체}.read_num {format},{offset}`


### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">format</td>
      <td style="text-align:left">
			바이너리 데이터 형식(format)<sup>*</sup><br>
      e.g. "U4", "s2"<br>
      </td>
      <td style="text-align:left">문자열형</td>
    </tr>
	 <tr>
      <td style="text-align:left">offset</td>
      <td style="text-align:left">
        데이터를 읽을 위치 (0-based byte offset)
      </td>
      <td style="text-align:left">정수형</td>
    </tr>
  </tbody>
</table>

<br>

\* [7.4.2 지원 형식 (format)](../2-format.md)을 참조하십시오.
<br>
<br>

### 리턴값

* 읽은 숫자형 값
* 만일 데이터 형식을 읽을 때 오류가 발생하면 0을 리턴합니다.


### 사용 예

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
print bbuf.read_num("F8", 0) # "9.80665"
print bbuf.read_num("U4", 12) # "3"
print bbuf.read_num("U4", 16) # "5"
```
# read_nums

### 설명

바이너리 버퍼의 지정 위치로부터 지정한 개수의 숫자형 값을 읽어 배열 형식으로 리턴합니다.


### 문법

`{BBuf객체}.read_num  {format},{offset},{n.item}`


### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">format</td>
      <td style="text-align:left">
			바이너리 데이터 형식(format)<sup>*</sup><br>
      e.g. "U4", "s2"
      </td>
      <td style="text-align:left">문자열형</td>
    </tr>
	  <tr>
      <td style="text-align:left">offset</td>
      <td style="text-align:left">
        데이터를 읽을 위치 (0-based byte offset)
      </td>
      <td style="text-align:left">정수형</td>
    </tr>
    <tr>
      <td style="text-align:left">n.item</td>
      <td style="text-align:left">
        읽을 데이터 개수
      </td>
      <td style="text-align:left">정수형</td>
    </tr>
  </tbody>
</table>

<br>


\* [7.4.2 지원 형식 (format)](../2-format.md)을 참조하십시오.
<br>
<br>


### 리턴값

* 읽은 숫자형 값들의 배열.  
* 만일 버퍼에 있는 데이터의 개수가 지정한 개수보다 적으면, 있는 만큼만 읽습니다.
* 만일 데이터 형식을 읽을 때 오류가 발생하면 빈 배열을 리턴합니다.


### 사용 예

```python
var bbuf=enet.BBuf()
bbuf.append("F8", 9.80665)
bbuf.append("U4", [2, 3, 5, 7, 11, 13])
print bbuf.read_nums("U4", 12, 3) # "[3, 5, 7]"
print bbuf.read_num("U4", 12, 6) # "[3, 5, 7, 11, 13]"
```
# 8. 앨리어스(alias)

앨리어스\(alias\)란 변수나 객체의 속성의 표기를 대체할 수 있는 이름입니다. 반복해 사용하기에 너무 긴 속성 표기를 간결한 이름으로 대체하거나, 특정한 인덱스의 IO 변수를 가독성이 좋은 이름으로 대체해 사용할 수 있습니다.

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
# 9. 파일

# 9.1 파일시스템

Hi6 제어기의 MAIN 모듈 파일시스템에서, 디렉토리와 파일의 생성, 복사, 삭제를 수행하는 명령문들을 설명합니다.
# 9.1.1 mkdir문

mkdir문은 디렉토리를 생성하는 프로시져입니다.

### 설명

MAIN 모듈에 지정한 경로의 디렉토리를 생성합니다.

- 티치펜던트나 USB메모리에는 생성할 수 없습니다.
- 중간 경로의 디렉토리가 존재하지 않으면, 중간 경로까지 만들어줍니다.

### 문법

```python
mkdir <경로>
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">경로</td>
      <td style="text-align:left">
        생성할 디렉토리 경로.<br>
        맨 앞에는 /를 붙이지 마십시오.
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
mkdir "work/data1"
```

![](../../_assets/mkdir.png)

# 9.1.2 copyfile문

copyfile문은 디렉토리나 파일의 복사를 요청하는 프로시져입니다.

### 설명

지정한 원본 경로의 디렉토리, 혹은 파일을 지정한 대상 경로파일명으로 복사합니다.   

- 티치펜던트나 USB 메모리가 아닌 MAIN 모듈 내에서만 수행할 수 있습니다.
- 대상 경로파일명의 중간 경로의 디렉토리가 존재하지 않으면, 중간 경로까지 만들어줍니다.
- 대상 디렉토리가 이미 존재하면 삭제 후 복사합니다.
- 대상 파일이 이미 존재하면 overwrite 합니다.
- 디렉토리의 서브 디렉토리들도 모두 복사됩니다.
- 경로파일명은 wildcard('*', '?')도 지원합니다.

- 용량이 큰 파일이나 디렉토리 전체가 복사될 수도 있기 때문에, 복사 중 대기에 의한 택트 타임 손실이 없도록 백그라운드에서 비동기적으로 수행됩니다. 즉, copyfile 명령문이 수행되면 백그라운드 작업에서 복사를 시작하면서 즉각 다음 명령문의 수행을 진행합니다. 가령, 복사를 요청해놓고 move문들을 실행할 수 있습니다. 복사가 성공적으로 완료 되었는지는 결과변수의 값을 읽어 확인 할 수 있습니다.  (즉, 복사가 실패해도 에러나 경고가 발생하지 않습니다.)
- 하나의 복사나 삭제가 끝나기 전에는 다른 복사나 삭제를 요청할 수 없습니다.


### 문법

```python
copyfile <결과변수>,<원본 경로파일명>,<대상 경로파일명>
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">결과변수</td>
      <td style="text-align:left">
        백그라운드 수행 결과<br>
        <ul>
        <li>1: 성공적으로 완료됨.</li>
        <li>0: 복사 진행 중.</li>
        <li>-1: 유효하지 않은 원본 경로파일명.</li>
        <li>-2: 유효하지 않은 대상 경로파일명.</li>
        <li>-3: 복사 실패.</li>
        <li>-6: wildcard 복사 시 전부 실패.</li>
        <li>-7: wildcard 복사 시 일부 실패.</li>
        <li>-11: 임시경로 생성 실패.</li>
        <li>-12: 임시경로로의 복사 실패.</li>
        <li>-13: 기존 대상경로 클리어 실패.</li>
        <li>-14: 대상경로 생성 실패.</li>
        <li>-15: 임시경로에서 대상경로로의 이동 실패.</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">원본 경로파일명</td>
      <td style="text-align:left">
        복사할 디렉토리 경로,<br>
        혹은 복사할 파일의 경로파일명
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
    <tr>
      <td style="text-align:left">대상 경로파일명</td>
      <td style="text-align:left">
        '/' 문자로 끝나면 복사될 경로.<br>
        '/' 문자로 끝나지 않으면 복사를 통해 생성될 경로파일명.
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
   var res
   copyfile res,"project/vars","work/vars_1" # vars_1/ 폴더가 생성됨.
   wait res==1,8,*timeout
   copyfile res,"project/vars","work/vars_1/" # vars_1/vars/ 폴더가 생성됨.
   wait res==1,8,*timeout
   copyfile res,"work/clear.job","project/jobs/0005_clear.job"
   wait res==1,4,*timeout
   copyfile res,"work/*_sub.job","project/jobs/" # wildcard
   wait res==1,4,*timeout
   call 5
   end
   *timeout
   print "copyfile failed"
   end
```

![](../../_assets/copyfile.png)

# 9.1.3 delfile문

delfile문은 디렉토리나 파일의 삭제를 요청하는 프로시져입니다.

### 설명

지정한 경로의 디렉토리, 혹은 파일을 삭제합니다.   

- 티치펜던트나 USB 메모리가 아닌 MAIN 모듈 내에서만 수행할 수 있습니다.
- 디렉토리의 서브 디렉토리들도 모두 삭제됩니다.
- 지정한 경로파일명이 존재하지 않으면, 성공으로 종료합니다.
- 경로파일명은 wildcard('*', '?')도 지원합니다.

- 용량이 큰 파일이나 디렉토리 전체가 삭제될 수도 있기 때문에, 삭제 중 대기에 의한 택트 타임 손실이 없도록 백그라운드에서 비동기적으로 수행됩니다. 삭제가 성공적으로 완료 되었는지는 결과변수의 값을 읽어 확인 할 수 있습니다. (즉, 복사가 실패해도 에러나 경고가 발생하지 않습니다.)
- 하나의 복사나 삭제가 끝나기 전에는 다른 복사나 삭제를 요청할 수 없습니다.


### 문법

```python
delfile <결과변수>,<경로파일명>
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">결과변수</td>
      <td style="text-align:left">
        백그라운드 수행 결과<br>
        <ul>
        <li>1: 성공적으로 완료됨.</li>
        <li>0: 삭제 진행 중.</li>
        <li>-41: 디렉토리 삭제 실패.</li>
        <li>-42: 파일 삭제 실패.</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">경로파일명</td>
      <td style="text-align:left">
        삭제할 디렉토리 경로,<br>
        혹은 삭제할 파일의 경로파일명
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
   var res
   delfile res,"work/vars_1"
   wait res==1,8,*timeout
   delfile res,"work2/10??.job" # wildcard
   wait res==1,8,*timeout
   copyfile res,"project/jobs/0005_sub.job"
   wait res==1,4,*timeout
   end
   *timeout
   print "delfile failed"
   end
```
# 9.2 load/save

Hi6 제어기 MAIN 모듈의 메모리로 파일을 불러오거나 저장하는 명령문들을 설명합니다. 
# 9.2.1 load_job문

MAIN 모듈의 project/jobs/ 폴더의 변경사항을 새로 메모리로 읽어들이는 명령문입니다.

### 설명

MAIN 모듈의 project/jobs/ 폴더의 job들을 새로 메모리로 로드합니다.

FTP나 copyfile 명령으로 .job파일들을 jobs/ 폴더 내에 복사 혹은 overwrite한 경우, 이 명령문을 수행해주어야만 메모리로 반영되어 선택이나 call을 할 수 있습니다.

- 주의: jobs/ 폴더에 존재하지 않는 메모리 내의 job은 삭제됩니다.
- 수정된 시각이 달라진 파일이면 로드됩니다.
- 메모리에 존재하지 않는 파일이면 로드됩니다.

- 용량이 큰 .job들이 로드될 수 있기 때문에, 로드에 의한 택트 타임 손실이 없도록 백그라운드에서 비동기적으로 수행됩니다. 로드가 성공적으로 완료 되었는지는 결과변수의 값을 읽어 확인 할 수 있습니다.
- 로드가 끝나기 전에는 또 다른 로드를 요청할 수 없습니다.


### 문법

```python
load_job <결과변수>,"*"
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">결과변수</td>
      <td style="text-align:left">
        백그라운드 수행 결과<br>
        <ul>
        <li>1: 성공적으로 완료됨.</li>
        <li>0: 로드 진행 중.</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">job 파일명</td>
      <td style="text-align:left">
        모든 파일을 뜻하는 "*" 인수만을 사용할 수 있습니다.
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
     var res
     copyfile res,"project/vars","work/vars_1"
     wait res==1,8,*timeout
     copyfile res,"work/sub5.job","project/jobs/0005_sub.job"
     wait res==1,4,*timeout
     load_job res,"*"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "copyfile failed"
     end
```
# 10. 기타

# 10.1 기타 프로시져

# 10.1.1 gather문

gather문은 데이터 수집 기능을 사용할 때 데이터 수집 시작과 종료 위치를 지정하는 프로시져입니다.

### 설명

gather를 통해 데이터를 수집 시작과 종료를 지정합니다. 수집 결과 파일은 아래와 같이 저장됩니다.
- 저장 경로: MAIN/project
- 파일명: 0001.GDT ~ 0030.GDT

수집 결과 파일은  최대 30개까지 저장되며, 개수 초과 시 이전 수집 결과 파일을 덮어써서 저장됩니다.


### 문법

```python
gather <시작/종료>
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">시작/종료</td>
      <td style="text-align:left">
        선택할 사용자 좌표계 번호<br>
        <ul>
        <li>1: 데이터 수집 시작</li>
        <li>0: 데이터 수집 종료</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
S1   move L,spd=100%,accu=0,tool=0
     gather 1
S2   move L,spd=100%,accu=0,tool=0
     delay 1.5
S3   move L,spd=100%,accu=0,tool=0
     gather 0
     end
```# 10.1.2 tonl문

tonl문은 시작과 종료 사이의 스텝들에 대해 위치보정을 수행하기 위한 프로시져입니다.

### 설명

좌표 변환 관계를 알고있는 경우, 별도의 좌표변환 관계 계산없이 변환관계를 입력하는 경우에 적용하는 기능입니다.  

R=[x,y,z,rx,ry,rz]

![](../../_assets/tonl2.png)

자세 행렬의 경우 Rot_z.Rot_y.Rot_x의 순서로 적용됩니다.

### 문법

```python
tonl <시작/종료>,<쉬프트량>
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">시작/종료</td>
      <td style="text-align:left">
        온라인 좌표변환 시작/종료<br>
        <ul>
        <li>on: 시작</li>
        <li>off: 종료</li>
        </ul>
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
    <tr>
      <td style="text-align:left">쉬프트량</td>
      <td style="text-align:left">
        복사할 디렉토리 경로,<br>
        혹은 복사할 파일의 경로파일명
      </td>
      <td style="text-align:left">쉬프트변수</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
   global sft
   enet1.recv msg #이더넷 통신으로 쉬프트량 수신
   sft=Shift(msg)
   tonl on,sft
   move L,spd=50mm/s,accu=0,tool=1
   move L,spd=10mm/s,accu=0,tool=1
   move L,spd=50mm/s,accu=0,tool=1
   tonl off
```

![](../../_assets/tonl.png)

# 10.1.3 triggout문

triggout문은 신호출력 시점을 선출(-) 혹은 후출(+)할 수 있게 조정할 수 있는 프로시져입니다.

### 설명

contpath 1이나 2로 설정되어 명령어를 연속 처리하는 구간에서 지령위치가 목표위치(Accuracy OK)에 도착하면  발생하는 신호출력 시점을 선출(-) 혹은 후출(+)할 수 있게 조정할 수 있습니다.   


### 문법

```python
triggout <출력변수>,val=<출력값>,time=<선출/후출 시간>
triggout <출력변수>,val=<출력값>,dist=<선출/후출 거리>,x=<X방향 절대위치>
triggout <출력변수>,val=<출력값>,dist=<선출/후출 거리>,y=<Y방향 절대위치>
triggout <출력변수>,val=<출력값>,dist=<선출/후출 거리>,z=<Z방향 절대위치>
triggout <출력변수>,val=<출력값>,time=<선출/후출 거리>,j=<축방향 절대위치>
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">출력변수</td>
      <td style="text-align:left">
        출력신호에 대응하는 변수<br>
        <ul>
        <li>범용출력에 대응하는 do, dob, dow, dol, dof 변수</li>
        <li>전용출력에 대응하는 so, sob, sow, sol, sof 변수</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">출력값</td>
      <td style="text-align:left">
        산술식,<br>
        단일신호 출력(do, so)의 경우 0이면 off, 0이 아니면 on
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">선출/후출 시간</td>
      <td style="text-align:left">
        -10.00 ~ 2.00 [s]<br>
        (-)인 경우 목표위치 도달전 신호가 출력되며 (+)인 경우 도달후 출력됩니다.
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">선출/후출 거리</td>
      <td style="text-align:left">
        -3000 ~ 3000 [mm]<br>
        목표위치 도달시 신호가 출력됩니다.
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
   move L,spd=300mm/s,accu=3,tool=1
   triggout do1,val=1,time=-0.5
   move L,spd=30%,accu=2,tool=1
   end
```
# 10.1.4 int_def문

int_def문은 인터럽트 조건과 감시 구간, 그리고 인터럽트 발생시 실행할 프로그램을 지정하는 프로시져입니다.

### 설명

인터럽트 기능이란 프로그램 호출의 한가지 종류입니다. 로봇이 인터럽트 감시 구간에서 작업할 경우, 기 정의된 인터럽트 조건을 만족하면 기 정의된 프로그램을 호출하여 실행합니다. 이 호출된 프로그램의 실행이 종료되면 다시 이전 실행하던 프로그램의 위치로 돌아와 계속 작업을 수행합니다.   

![](../../_assets/int_def_1.png)


### 기능 요약

- 인터럽트 감시 구간에서만 동작합니다.
- 인터럽트 조건식으로는 산술식을 모두 지원합니다.
- 인터럽트 프로그램 수행 중 또 다른 인터럽트 처리(다중 인터럽트)도 허용합니다.


### 인터럽트 삭제시점
하기의 조작이 발생되는 경우에는 모든 정의된 인터럽트가 자동으로 삭제됩니다.
- 'R0 : 태스크 리셋' 수행시
- 프로그램의 처음 실행시 
- 스텝이나 펑션 변경후 기동시


### 문법

```python
int_def <on/off>,no=<인터럽트 번호>,var=<인터럽트 조건>,val=<조건 일치값>,job=<호출 프로그램>,[once]
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">on/off</td>
      <td style="text-align:left">
        인터럽트를 정의하거나 정의된 인터럽트를 삭제<br>
        <ul>
        <li>on: 새로운 인터럽트 정의.</li>
        <li>off: 정의된 인터럽트 삭제. (3번째 이후의 파라미터 무시됨)</li>
        </ul>
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
    <tr>
      <td style="text-align:left">인터럽트 번호</td>
      <td style="text-align:left">
        정의 또는 삭제할 인터럽트 번호를 지정<br>
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">인터럽트 조건</td>
      <td style="text-align:left">
        인터럽트를 발생시킬 조건식을 정의<br>
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">조건 일치값</td>
      <td style="text-align:left">
        인터럽트 발생을 위한 인터럽트를 조건식의 값<br>
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">호출 프로그램</td>
      <td style="text-align:left">
        인터럽트 발생시 호출할 프로그램 번호<br>
      </td>
      <td style="text-align:left">산술식</td>
    </tr>
    <tr>
      <td style="text-align:left">[once]]</td>
      <td style="text-align:left">
        옵션 파라미터로 인터럽트 감시 구간내에서 인터럽트가 수회 발생하더라도 모두 처리하지 않고 처음 발생한 인터럽트 1회만 처리하고자 할때 사용<br>
      </td>
      <td style="text-align:left">문자열식</td>
    </tr>
  </tbody>
</table>


### 에러 가이드

- E1351 : 이미 정의된 인터럽트 번호에 대해서 삭제없이 재정의하는 경우에 발생합니다. 작성된 프로그램을 확인하십시오.


### 사용 예

```python
   int_def on,no=1,var=di5,val=1,job=24,once #인터럽트 정의
   move P,spd=30%,accu=3,tool=1
   move L,spd=30mm/s,accu=3,tool=1
   ...
   move L,spd=30mm/s,accu=3,tool=1
   move P,spd=30%,accu=3,tool=1
   int_def off,no=1 #인터럽트 삭제
   move P,spd=30%,accu=3,tool=1
   end
```


# 10.2 기타 함수

# 10.2.1 rducs함수 - 사용자좌표계

### 설명

생성된 사용자좌표계를 포즈로 읽는 명령어입니다.   

- 생성된 사용자 좌표계의 위치/방향이 해당 포즈 값으로 복사합니다.
- 생성되지 않았거나 파라미터가 유효하지 않은 경우, 에러가 발생하면서 job 실행이 중단됩니다.


### 문법

```python
<결과변수> = rducs(<사용자좌표계 번호>,<포즈변수>)
```

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">결과변수</td>
      <td style="text-align:left">
        백그라운드 수행 결과<br>
        <ul>
        <li>0: 성공적으로 완료됨.</li>
        </ul>
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">사용자좌표계 번호</td>
      <td style="text-align:left">
        읽을 사용자좌표계의 번호
      </td>
      <td style="text-align:left">[1~20]</td>
    </tr>
    <tr>
      <td style="text-align:left">포즈변수</td>
      <td style="text-align:left">
        복사할 포즈변수
      </td>
      <td style="text-align:left">포즈변수</td>
    </tr>
  </tbody>
</table>

### 리턴값


<table>
  <thead>
    <tr>
      <th style="text-align:left">값</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>
        성공
      </td>
      <td></td>
    </tr>  
  </tbody>
</table>


### 에러 가이드

- E14613 : 설정된 파라미터가 지정된 형식과 맞지 않을 때 발생합니다. 설정된 파라미터를 확인하십시오.
- E14614 : 사용자좌표번호가 숫자가 아닐때 발생합니다. 사용자좌표번호를 다시 지정하십시오.
- E14615 : 사용자좌표번호가 1~20 사이의 숫자가 아닐 때 발생합니다. 사용자좌표번호를 변경하십시오.
- E1336 : 등록되지 않은 사용자좌표번호인 경우에 발생합니다. 사용자좌표번호를 변경하십시오.


### 사용 예

```python
   var p_uc2=Pose(0,0,0,0,0,0,"base")
   var uc2=rducs(2,p_uc2)
   end
```

![](../../_assets/rducs.png)

# 10.2.2 segment 함수

segment 함수는 시작위치와 종료위치간의 거리를 균등 분할하는 함수입니다.

### 설명

함수 인자의 시작위치와 종료위치간의 거리를 균등 분할하여 지정한 카운터에 해당하는 위치, 자세를 고려한 포즈 값을 포즈변수에 저장합니다.
![](../../_assets/image_segment_1.png)

예를 들어 P3=segment(P1,P2,3,2) 인 경우, 
P1시작위치에서 P2목표위치간의 거리를 3등분하여 지정한 2번째 포즈의 위치와 자세를 고려한 포즈 값을 P3 포즈변수에 저장합니다.

함수의 인자에 경유위치를 추가하면, 시작위치와 경유점, 목표위치로 이루어진 원호상의 거리를 균등 분할하여 지정한 카운터에 위치, 자세를 고려한 포즈 값을 포즈변수에 저장합니다.

![](../../_assets/image_segment_2.png)

예를 들어 P10=segment(P1,P2,P3,4,2) 인 경우,
P1시작포즈, P2 경유포즈 P3목표포즈로 이루어진 원호상의 거리를 4등분하여 지정한 2번째 포즈의 위치와 자세를 고려한 포즈 값을 P10 포즈변수에 저장합니다.
<br><br>

### 문법

```python
result=segment(<시작포즈>,<종료포즈>,<분할 수>,<카운터>)
```

```python
result=segment(<시작포즈>,<경유포즈>,<종료포즈>,<분할 수>,<카운터>)
```

### 파라미터
<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">시작포즈</td>
      <td style="text-align:left">
        시작 위치
      </td>
      <td style="text-align:left">포즈변수</td>
    </tr>
    <tr>
      <td style="text-align:left">경유포즈</td>
      <td style="text-align:left">
        경유 위치
      <td style="text-align:left">포즈변수</td>
    </tr>
    <tr>
      <td style="text-align:left">종료포즈</td>
      <td style="text-align:left">
        종료 위치
      </td>
      <td style="text-align:left">포즈변수</td>
    </tr>
    <tr>
      <td style="text-align:left">분할 수</td>
      <td style="text-align:left">
        분할 수<br>
        (1 ~ 30000)
      </td>
      <td style="text-align:left">변수</td>
    </tr>
    <tr>
      <td style="text-align:left">카운터</td>
      <td style="text-align:left">
        저장할 포즈의 카운터 번호<br>
        (0 ~ 300000, 0: 시작포즈)
      </td>
      <td style="text-align:left">변수</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
     var po1,po2,po3
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000) # 시작포즈
     po2=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000) # 종료포즈
     po3=segment(po1,po2,4,2)
     end
```

```python
     var po1,po2,po3,po10
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000) # 시작포즈
     po2=Pose(1500.000,500.000,1938.000,0.000,0.000,0.000) # 경유포즈
     po3=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000) # 종료포즈
     po10=segment(po1,po2,po3,5,3)
     end
```# 10.2.3 intersection 함수

intersection 함수를 사용하면 직선과 한 점의 최단거리로 만나는 점을 구하거나, 두 직선을 지나는 최단거리 직선과의 교점을 구할 수 있습니다.

### 설명

함수 인자에 직선을 이루는 두 점과 그 외의 한 점을 지정하면, 직선과 한 점을 최단거리로 연결하는 직선의 교차포즈를 구합니다.

![](../../_assets/image_intersection_1.png)

함수 인자에 직선을 이루는 두 점과 다른 직선을 이루는 두 점을 지정하면, 두 직선을 최단거리로 만나는 직선과의 교점을 구할 수 있습니다. 교점은 첫번째로 지정한 직선과의 만나는 점입니다.

![](../../_assets/image_intersection_2.png)

### 문법

```python
result=intersection(<직선참조포즈 1>,<직선참조포즈 2>,<위치참조포즈>)
```

```python
result=intersection(<직선참조포즈 1>,<직선참조포즈 2>,<직선참조포즈 3>,<직선참조포즈 4>)
```

### 파라미터
<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">직선참조포즈 1</td>
      <td style="text-align:left">
        첫번째 직선을 얻기 위한 첫번째 참조포즈
      </td>
      <td style="text-align:left">포즈변수</td>
    </tr>
    <tr>
      <td style="text-align:left">직선참조포즈 2</td>
      <td style="text-align:left">
        첫번째 직선을 얻기 위한 두번째 참조포즈
      <td style="text-align:left">포즈변수</td>
    </tr>
    <tr>
      <td style="text-align:left">위치참조포즈</td>
      <td style="text-align:left">
        직선과 최단거리 위치를 구하기 위해 참조하는 포즈
      </td>
      <td style="text-align:left">포즈변수</td>
    </tr>
    <tr>
      <td style="text-align:left">직선참조포즈 3</td>
      <td style="text-align:left">
        두번째 직선을 얻기 위한 첫번째 참조포즈
      </td>
      <td style="text-align:left">포즈변수</td>
    </tr>
    <tr>
      <td style="text-align:left">직선참조포즈 4</td>
      <td style="text-align:left">
        두번째 직선을 얻기 위한 두번째 참조포즈
      </td>
      <td style="text-align:left">포즈변수</td>
    </tr>
  </tbody>
</table>

### 사용 예

```python
     var po1,po2,po3,result
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000)
     po2=Pose(2000.000,0.000,1938.000,0.000,0.000,0.000)
     po3=Pose(2500.000,500.000,1938.000,0.000,0.000,0.000)
     result=segment(po1,po2,po3)
     end
```

```python
     var po1,po2,po3,po4,result
     po1=Pose(1000.000,0.000,1938.000,0.000,0.000,0.000)
     po2=Pose(1500.000,500.000,1938.000,0.000,0.000,0.000)
     po3=Pose(2000.000,0.000,2000.000,0.000,0.000,0.000)
     po3=Pose(2000.000,0.000,2000.000,0.000,0.000,0.000)
     result=segment(po1,po2,po3,po4)
     end
```# 10.3 시스템 변수
# 10.3.1 _int.no 변수

_int.no 시스템 변수는 발생한 인터럽트 번호를 관리합니다.

### 설명

int_def문의 조건식이 만족되어 인터럽트가 발생했을 때 호출하는 프로그램은 동일할 수 있으므로 호출된 프로그램에서 어떤 인터럽트 조건이 발생되었는지 확인하고자 할 때 사용할 수 있습니다.


### 문법

```python
var res
res = _int.no
```


### 사용 예

```python
   ...
   if _int.no==1  #인터럽트 번호 1 발생이면
   print "센서 1 동작으로 인터럽트 발생됨"
   else if _int.no==2 #인터럽트 번호 2 발생이면
   print "센서 2 동작으로 인터럽트 발생됨"
   stop #로봇 정지
   endif
   ...
   end
```


# 9.1.2 _int.target문

_int.target 시스템 변수는 로봇의 목표위치 도달 상태를 조정합니다.

### 설명

move문에서 로봇이 이동중에 인터럽트가 발생하여 호출 프로그램의 실행이 종료된 후 이전 실행하던 프로그램의 위치로 되돌아 올 때 이 위치를 조정하기 위해서 사용합니다.   


### 문법

```python
_int_target=1
```

### 사용 예

```python
- _int.target=-1
```

![](../../_assets/int_target_1.png)


```python
- _int.target=1 or 0
```
![](../../_assets/int_target_2.png)

# 10.3.3 _tool 변수

### 설명

툴데이터를 읽거나 변경하기 위한 시스템 변수입니다.   

- 생성된 툴데이터(무게/중심/이너셔)를 읽거나 해당 툴데이터를 변경합니다.
- 툴데이터가 생성되지 않았거나 맴버가 유효하지 않은 경우, 에러가 발생하면서 job 실행이 중단됩니다.


### 문법

```python
<쉬프트변수> = _tool3
_tool3 = <쉬프트변수>
_tool[3] = <쉬프트변수>
_tool[5].mass = <산술변수>
_tool[5].cx = <산술변수>
_tool[5].cy = <산술변수>
_tool[5].cz = <산술변수>
_tool[5].ixx = <산술변수>
_tool[5].iyy = <산술변수>
_tool[5].izz = <산술변수>
```


### 에러 가이드

- E14550 : 툴데이터의 맴버가 유효하지 않은 경우 발생합니다. 설정된 툴데이터의 맴버가 mass, cx, cy, cz, ixx, iyy, izz인지 확인하십시오.
- E14286 : 대입문 우변으로 쉬프트변수가 아닌 경우이거나 툴변수의 맴버가 유효하지 않은 경우에 발생합니다. 대입문 우변을 다시 지정하십시오.


### 사용 예

```python
   var sft=Shift(100,20,30,0,0,0,"tool")
   _tool3=sft
   move L,spd=30%,accu=1,tool=3
   end
```

![](../../_assets/_tool.png)

