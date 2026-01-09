# 5.10 softxyz 문

센서리스 힘제어 기능으로, 사용자가 설정한 환경에서 로봇이 외력에 대해 직교좌표 기준으로 유연하게 움직이도록 하는 기능입니다.

정확한 동작을 위해 툴 데이터와 부가중량 정보를 반드시 올바르게 설정해야 합니다.

{% hint style="warning" %}

softxyz 기능은 **힘 센서를 사용하지 않는 기반 기능**이기 때문에,  
부드럽고 자연스러운 모션 구현에는 **물리적 한계가 존재**합니다.

다만, `softxyz_lim` 설정값을 작업 환경에 맞게 적절히 조절하면  
최대한 부드러운 모션을 구현할 수 있습니다.

`softxyz_lim (pos / xnr / vel / thr)` 값은 로봇이 외력에 반응하는 정도를 직접적으로 결정하므로,   환경, 조립 공정, 툴 강성 등에 따라 **세밀한 튜닝이 필요**합니다.

{% endhint %}

### 설명 
* 센서를 사용하지 않고 외력에 대해 직교좌표 기준으로 로봇이 밀리는 기능 


### 문법 
```python
softxyz on, crd=<기준좌표계>
softxyz set, dpr=<강성>
softxyz off
```

### 파라미터 
- **on** : softxyz 기능 시작  
- **off** : softxyz 기능 종료  
- **set** : softxyz 설정값 변경  

- **crd** : 외력 반응 기준 좌표계  
  - 사용 가능: `base`, `robot`, `tool`, `user_x`

- **dpr** : 강성(Stiffness) 값  
  - 범위: **0.0 ~ 2.0**  
  - 값이 **클수록 단단해져 외력에 덜 밀림**  
  - 기본값: **1.0**
```python
softxyz on,  crd="base"     # 베이스 좌표계 기준
softxyz on,  crd="robot"    # 로봇 좌표계 기준
softxyz on,  crd="tool"     # 툴 좌표계 기준
softxyz on,  crd="user_1"   # 사용자 정의 좌표계 1번

softxyz set, dpr=1.0        # 강성값 설정 (0.0~2.0, 값이 클수록 단단함)
softxyz off                  # 기능 종료 
```


### 사용 예 
> 예제1) Z방향으로 조립하기 위해 X, Y, Ry 방향으로 밀릴 수 있도록 한 경우  
> * 좌표계 : 로봇좌표계 기준 (crd="robot") <br>
> * 이동 위치(xnr) 제한 설정 : X, Y방향으로 [-50,+50] 범위(mm), Ry방향 [-3,+3] 범위(deg) <br>
> * 속도(vel) 제한 설정 : X, Y방향으로 최대 5mm/sec, Ry방향으로 3deg/sec 밀리도록 설정 <br>
> * 문턱값(thr) 제한 설정 : X방향 3N, Y방향 3N 그리고 Ry방향 1Nm 

```python
S1   move P,spd=100mm/sec,accu=0,tool=0
     delay 2.0 # softxyz on 하기 전에 delay 설정 필수  
     softxyz_lim xnr, x=50, y=50, ry=3
     softxyz_lim vel, x=5, y=5, ry=3
     softxyz_lim thr, x=20, y=20, ry=3
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
     softxyz_lim pos, _y=300, y_=200
     softxyz_lim vel, y=150
     softxyz on, crd="robot"
S2   wait ... 
     softxyz off 
     end 
```

--- 
> **정보**
>
> - `softxyz on`을 사용하기 전에 **반드시** `softxyz_lim` 명령을 통해  
>   `pos`, `xnr`, `vel`, `thr` 값을 설정해야 합니다.  
>   (최대 밀림 거리, 속도, 직교좌표 문턱값 설정 필수)
>
> - 외력 민감도를 높이기 위해 `softxyz on` 실행 전에  
>   **delay 명령으로 1~2초 동안 로봇을 정지**시켜 두는 것이 좋습니다.
>
> - softxyz 동작 중 떨림이 발생할 경우 다음과 같은 조치를 권장합니다.
>   1) *thr 값을 높인다*  
>   2) *dpr 값을 높인다*  
>   3) *vel 값을 낮춘다*

