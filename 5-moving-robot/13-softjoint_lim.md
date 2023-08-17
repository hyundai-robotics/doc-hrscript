# 5.13 softjoint_lim

softjoint_lim 명령어는 softjoint on 기능 사용 전 파라미터 값을 미리 설정 해야 한다. <br>

사용자는 활성화 되는 축 번호, 부드러움, 각도 제한 값 그리고 문턱값 등을 설정 해야 한다. 

--- 

## 설명 
* softjoint 파라미터 설정 명령어  


## 문법 
```python
softjoint_lim, j=<축번호>, sft=<부드러움 정도>, ang=<각도 범위>, thr=<문턱값> 
```

## 파라미터 
* j : 축 번호 [1~6]
* sft : 값이 클 수록 더 유연하게 움직임[0:off,0~100]
* ang : 각도 제한 범위 [deg]
* thr : 문턱 값[Nm]


## 사용 예 
> 예제1) 3번 축 방향 파라미터 설정 
> * 3번 축 활성화, 부드러움(50), 각도 제한 -30~30(deg) 그리고 문턱값10(Nm)   
```python
softjoint_lim, j=3, sft=50, ang=30, thr=10
```

> 예제) 2번과 3번 축 방향으로 밀릴 수 있도록 한 경우
> * 부드러움(sft) 설정 : 2번 축 sft(30), 3번 축 sft(80)  
> * 각도(ang) 제한 설정 : 2번 축 [-50,+50] 범위(deg), 3번 축 제한 없음<br>
> * 문턱값(thr) 제한 설정 : 2번 축 3(Nm), 3번 축 5(Nm) 


```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0 # softjoint on 하기 전에 delay 설정 필수  
     softjoint_lim j=2,sft=30,ang=50,thr=3
     softjoint_lim j=3,sft=80,thr=5
     softjoint on
S2   move P,spd=250mm/sec,accu=0,tool=0
     softjoint off 
     end 
```


--- 
{% hint style="info" %}

* softjoint_lim 파라미터는 축 번호와 부드러움 정도는 필수적으로 설정해야 하지만, 각도 범위와 문턱값은 설정을 하지 않으면 각도를 제한하지 않고 문턱값은 0.0[Nm]로 자동 설정 된다. 

{% endhint %}
