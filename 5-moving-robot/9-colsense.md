# 5.9 colsense 문

모델기반 충돌검지 기능이 유효로 설정되어 있는 상태에서 로봇의 충돌검지 민감도를 설정합니다. 

모델기반 충돌검지 기능의 유/무효 설정과 기본 및 축별 민감도는 \[3: 로봇 파라미터 &gt; 14: 충돌 검지 &gt; 1: 모델기반충돌검지 \] 

메뉴에서 설정합니다. (이 메뉴는 충돌검지 기능을 사용할 수 있는 로봇이 선택된 경우에만 나타납니다.)

--- 

## 설명 
* 모델기반 충돌검지 기능 중 기본 민감도(general, sensitivity)를 조절 할 수 있습니다.
* 모델기반 충돌검지 기능 중 축별 민감도(axis, criteria)를 조절 할 수 있습니다. 


## 문법 
```python
colsense general,sensitivity=<기본 민감도>  
colsense axis,id=<축 번호>,criteria=<축별 민감도> 
```

## 파라미터 
* 기본 민감도(sensitivity)는 0~200까지 설정 가능하며, 값이 높을수록 충돌에 예민하게 반응.(기본 민감도=0, 충돌검지 기능 무효)
* 축 번호(id)는 로봇의 축 번호를 의미 S축 부터 R1축 까지 순서 대로 1~6으로 대입 한다.   
* 축별 민감도(criteria)는 0~100까지 설정 가능하며, 값이 낮을수록 충돌에 예민하게 반응.(축별 민감도=0, 해당 축만 충돌검지 기능 무효)


## 사용 예 
* 모델 기반 충돌검지 기능이 유효로 설정되어 있고, 작업 프로그램이 아래와 같으면 

```python
S1   move P,spd=60%,accu=0,tool=0
S2   move P,spd=60%,accu=0,tool=0
     colsense general,sensitivity=150
S3   move P,spd=60%,accu=0,tool=0
     colsense general,sensitivity=200
S4   move P,spd=60%,accu=0,tool=0
S5   move P,spd=60%,accu=0,tool=0
     colsense axis,id=1,criteria=0
     colsense axis,id=2,criteria=0
S6   move P,spd=60%,accu=0,tool=0
S7   move P,spd=60%,accu=0,tool=0
     end 
```
* S1과 S2는 \[3: 로봇 파라미터 &gt; 14: 충돌 검지 &gt; 1: 모델기반충돌검지 \] 메뉴에서 설정된 기본/축별 민감도로 충돌을 검지 한다. 
* S3의 기본 민감도는 150으로 설정되어 충돌을 검지하고, S4와 S5는 기본 민감도가 200으로 설정되어 충돌을 검지한다. 
* S6와S7에서는 S축과 H축에 대한 충돌을 검지 하지 않고, 나머지 축은 기본 민감도가 200으로 설정되어 충돌을 검지 한다. 

--- 
{% hint style="info" %}

축 별 최종 민감도값은 축별 민감도 값에 비례하고, 축 전체 기본 민감도와 반비례 합니다.    
{% endhint %}


