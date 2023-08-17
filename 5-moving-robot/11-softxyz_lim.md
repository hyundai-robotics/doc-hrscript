# 5.11 softxyz_limit 문

softxyz_lim 명령어는 softxyz on 기능 사용 전 파라미터 값을 미리 설정 해야 한다. <br>

사용자는 활성화 되는 로봇의 직교좌표 거리 제한, 위치, 속도 및 문턱값등을 설정 할 수 있다.    

--- 

## 설명 
* softxyz 파라미터 설정 명령어  


## 문법 
```pythonghlt
softxyz_lim pos,_x=<+X거리>,x_=<-X거리>,_y=<+Y거리>,y_=<-Y거리>,_z=<+Z거리>,z_=<-Z거리> 
softxyz_lim vel,x=<X속도>,y=<Y속도>,z=<Z속도>,rx=<Rx속도>,ry=<Ry속도>,rz=<Rz속도> 
softxyz_lim xnr,x=<X거리>,y=<Y거리>,z=<Z거리>,rx=<Rx거리>,ry=<Ry거리>,rz=<Rz거리> 
softxyz_lim thr,x=<X문턱값>,y=<Y문턱값>,z=<Z문턱값>,rx=<Rx문턱값>,ry=<Ry문턱값>,rz=<Rz문턱값> 
```

## 파라미터 
* softxyz_lim pos : 로봇이 이동할 수 있는 직교좌표 최대 거리를 설정 (X,Y,Z방향) [mm] 
* softxyz_lim vel : 로봇이 동작하는 직교좌표 최대 속도를 설정 (X,Y,Z,Rx,Ry,Rz방향) [mm/sec] or [deg/sec] 
* softxyz_lim xnr : 로봇이 이동할 수 있는 직교좌표 최대 거리와 각도를 제한 (X,Y,Z,Rx,Ry,Rz방향) [mm] or [deg] <br> 
  (로봇의 최대 동작영역은 pos와 xnr의 합집합으로 결정됨)  
* softxyz_lim thr : 로봇이 이동하기 위한 직교좌표 힘 문턱값을 설정 (X,Y,Z,Rx,Ry,Rz방향) [N] or [Nm]


## 사용 예 
> * +X방향200[mm], -Y방향100[mm], +Z방향300[mm]로 이동하는 최대 거리를 설정  
```python
softxyz_lim pos, _x=200, y_=100, _z=300
```
> * Z방향 최대 이동 속도를 40mm/sec로 설정 
```python
softxyz_lim vel, z=40
```
> * X방향으로 이동하는 최대 거리를 -200[mm]에서 200[mm]로 설정 
```python
softxyz_lim xnr, x=200
```
> * 직교좌표 Y방향의 힘 문턱값을 10[N]으로 설정 
```python
softxyz_lim thr, y=10
```


