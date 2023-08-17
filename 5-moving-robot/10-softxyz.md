# 5.10 softxyz 문

센서리스 힘제어 기능으로 사용자가 설정한 환경에서 로봇이 외력에 대해 직교좌표로 유연하게 움직이는 기능입니다. <br>

정확한 기능 사용을 위해 로봇에 부착된 툴 or 부가 중량 정보를 올바르고 정확하게 설정해야 합니다.


--- 

## 설명 
* 센서를 사용하지 않고 외력에 대해 직교좌표 기준으로 로봇이 밀리는 기능 


## 문법 
```python
softxyz on, crd=<기준좌표계>
softxyz off  
```

## 파라미터 
* on : 기능 시작, off : 기능 종료 
* crd : 로봇이 밀리는 기준 좌표계 (베이스, 로봇, 툴, 사용자 좌표계)
```python
softxyz on, crd="base"   #베이스 좌표계
softxyz on, crd="robot"  #로봇 좌표계
softxyz on, crd="tool"   #툴 좌표계
softxyz on, crd="user_1" #1번 사용자 좌표계 
softxyz off  
```


## 사용 예 
> 예제1) Z방향으로 조립하기 위해 X, Y, Ry 방향으로 밀릴 수 있도록 한 경우  
> * 좌표계 : 로봇좌표계 기준 (crd="robot") <br>
> * 이동 위치(xnr) 제한 설정 : X, Y방향으로 [-50,+50] 범위(mm), Ry방향 [-3,+3] 범위(deg) <br>
> * 속도(vel) 제한 설정 : X, Y방향으로 최대 5mm/sec, Ry방향으로 3deg/sec 밀리도록 설정 <br>
> * 문턱값(thr) 제한 설정 : X방향 3N, Y방향 3N 그리고 Ry방향 1Nm 

```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0 # softxyz on 하기 전에 delay 설정 필수  
     limit xnr, x=50, y=50, ry=3
     limit vel, x=5, y=5, ry=3
     limit thr, x=3, y=3, ry=1
     softxyz on, crd="robot"
S2   move P,spd=250mm/sec,accu=0,tool=0
     softxyz off 
     end 
```

> 예제2) 사출물 핸들링 
> * 좌표계 : 로봇좌표계 기준 (crd="robot") <br>
> * 위치(pos) 제한 설정 : +Y방향으로 최대 300mm까지, -Y방향으로 최대 200mm 까지 이동 <br>
> * 속도(vel) 제한 설정 : Y방향으로 최대 150mm/sec 속도로 밀리도록 설정 <br>

```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0 # softxyz on 하기 전에 delay 설정 필수  
     limit pos, _y=300, y_=200
     limit vel, y=150
     softxyz on, crd="robot"
S2   wait ... 
     softxyz off 
     end 
```

--- 
{% hint style="info" %}

* softxyz on으로 기능을 사용하기 전에 limit 명령문을 사용하여 pos, xnr, vel, thr 명령어로 최대 밀림거리, 속도 및 직교좌표 문턱값 등을 설정 해야 합니다. 

* 외력에 대한 로봇 민감도를 향상시키기 위해 softxyz on 명령어 전에 반드시 delay 명령어로 로봇을 1~2초 가량 정지시켜 놓는 것이 좋습니다. 

{% endhint %}
