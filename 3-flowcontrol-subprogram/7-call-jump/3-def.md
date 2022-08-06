# 3.7.3 def문 (사용자함수 정의)

V60.XX.XX부터.

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
