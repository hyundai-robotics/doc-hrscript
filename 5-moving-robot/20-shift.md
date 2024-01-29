# 5.20 shift문

shift문은 이미 티칭된 포인트를 XYZ 좌표계에서 툴 각도를 유지하면서 평행 이동하는 기능입니다.

### 문법
```python
"shift crd=<기준좌표계>,x=<X시프트량>,y=<Y시프트량>,z=<Z시프트량>
```

## 파라미터 
* crd : 기준좌표계["base":베이스, "robot":로봇, "tool":툴, "joint":축,"u":사용자]
* x,y,z : X,Y,Z시프트량[0~3000,mm]

## 사용 예 
```python
     var po1=Pose(0.691,99.293,24.758,-6.528,-48.574,15.774,0.000)
S1   move P,tg=po1,spd=10%,accu=0,tool=0
     shift crd="base",x=200,z=100
S2   move P,tg=po1,spd=10%,accu=0,tool=0
     shift crd="u1",x=-150,y=70,z=10
S3   move P,tg=po1,spd=10%,accu=0,tool=0
     end
```