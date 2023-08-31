# 5.11 softxyz_lim

Before using instruction "softxyz on", user should set softxyz_lim parameters such as position limit(pos), workspace limit(xnr), velocity limit(vel) and force threshold limit(thr). <br>


--- 

### Description 
* softxyz_lim parameter setting   


### Syntax 
```pythonghlt
softxyz_lim pos,_x=<+X>,x_=<-X>,_y=<+Y>,y_=<-Y>,_z=<+Z>,z_=<-Z> 
softxyz_lim vel,x=<X>,y=<Y>,z=<Z>,rx=<Rx>,ry=<Ry>,rz=<Rz>  
softxyz_lim xnr,x=<X>,y=<Y>,z=<Z>,rx=<Rx>,ry=<Ry>,rz=<Rz> 
softxyz_lim thr,x=<X>,y=<Y>,z=<Z>,rx=<Rx>,ry=<Ry>,rz=<Rz> 
```

### Parameter 
* softxyz_lim pos : Position limit based on cartesian space [mm] <br>
* softxyz_lim vel : Maximum translation and rotation velocity limit based on cartesian space [mm/sec] or [deg/sec] 
<br>
* softxyz_lim xnr : Workspace (position/rotation) limit based on cartesian space [mm] or [deg] <br>
* softxyz_lim thr : force threshold limit based on cartesian space [N] or [Nm] <br>


### Example
> * setting position limit : +X direction is 200[mm], -Y direction is 100[mm], +Z direction is 300[mm]
```python
softxyz_lim pos, _x=200, y_=100, _z=300
```
> * setting velocity limit : maximum speed of Z direction is 40[mm/sec] 
```python
softxyz_lim vel, z=40
```
> * setting workspace limit : maximum position of X direction is [-200,200][mm]
```python
softxyz_lim xnr, x=200
```
> * setting torque limit : torque threshold is set to 10[N]
```python
softxyz_lim thr, y=10
```


