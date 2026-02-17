# 5.11 `softxyz_lim`

在使用指令 `softxyz on` 之前，用户应设置 `softxyz_lim` 参数，如位置限制(`pos`)、工作空间限制(`xnr`)、速度限制(`vel`)和力阈值限制(`thr`). <br>

--- 

### 描述 
* softxyz_lim 参数设置   

### 语法 
```pythonghlt
softxyz_lim pos,_x=<+X>,x_=<-X>,_y=<+Y>,y_=<-Y>,_z=<+Z>,z_=<-Z> 
softxyz_lim vel,x=<X>,y=<Y>,z=<Z>,rx=<Rx>,ry=<Ry>,rz=<Rz>  
softxyz_lim xnr,x=<X>,y=<Y>,z=<Z>,rx=<Rx>,ry=<Ry>,rz=<Rz> 
softxyz_lim thr,x=<X>,y=<Y>,z=<Z>,rx=<Rx>,ry=<Ry>,rz=<Rz> 
```

### 参数 
* softxyz_lim pos : 基于笛卡尔空间的位置信限制 [mm] <br>
* softxyz_lim vel : 基于笛卡尔空间的最大平移和旋转速度限制 [mm/sec] 或 [deg/sec] 
<br>
* softxyz_lim xnr : 基于笛卡尔空间的工作空间 (位置/旋转) 限制 [mm] 或 [deg] <br>
* softxyz_lim thr : 基于笛卡尔空间的力阈值限制 [N] 或 [Nm] <br>

### 示例
> * 设置位置限制 : +X 方向为 200[mm], -Y 方向为 100[mm], +Z 方向为 300[mm]
```python
softxyz_lim pos, _x=200, y_=100, _z=300
```
> * 设置速度限制 : Z 方向的最大速度为 40[mm/sec] 
```python
softxyz_lim vel, z=40
```
> * 设置工作空间限制 : X 方向的最大位置为 [-200,200][mm]
```python
softxyz_lim xnr, x=200
```
> * 设置扭矩限制 : 扭矩阈值设定为 10[N]
```python
softxyz_lim thr, y=10
```