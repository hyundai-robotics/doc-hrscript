# _triggout.w241_enable 변수

_triggout.w241_enable은 거리 기반 triggout 명령어 사용 시, 신호 출력 성공 여부 판단에 실패했을 때 발생하는 경고 메시지를 켜고 끌 수 있는 시스템 변수입니다. 

### 설명

0또는 1의 값을 설정 할수 있으며, default값은 1입니다.

V70.04-00부터 지원됩니다.

### 문법

```python
_triggout.w241_enable=0
```

### 사용 예

```python
     # 경고 출력 기능 비활성화, 제어기 부팅시 default 값은 1 
     triggout.w241_enable=0
     
     print "warning mode = ",_triggout.w241_enable
     
     var cmd_dist=-20
     do20=0
     
S1   move P,spd=30%,accu=0,tool=0  
     delay 1
S2   move P,spd=cmd_spd%,accu=cmd_acc,tool=0 
     
     #---------------------------
     triggout do20,val=1,dist=cmd_dist,j=5
     #---------------------------
     
S3   move P,spd=cmd_spd%,accu=cmd_acc,tool=0  
S4   move P,spd=cmd_spd%,accu=cmd_acc,tool=0  
     delay 1
     end
```
