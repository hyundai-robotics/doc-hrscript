# 5.20 `shift`

### 描述
`shift` 语句在保持工具方向（工具角度）的同时，转换在 XYZ 坐标系统中已经教好的点。

### 语法
```python
shift crd=<参考坐标>,x=<X 移动值>,y=<Y 移动值>,z=<Z 移动值>
```

### 参数
* crd : 参考坐标系统  
["base": 基础, "robot": 机器人, "tool": 工具, "joint": 关节, "u": 用户]
* x, y, z : X, Y, Z 移动值 [0-3000, mm]

### 示例
```python
     var po1=Pose(0.691,99.293,24.758,-6.528,-48.574,15.774,0.000)
S1   move P,tg=po1,spd=10%,accu=0,tool=0
     shift crd="base",x=200,z=100
S2   move P,tg=po1,spd=10%,accu=0,tool=0
     shift crd="u1",x=-150,y=70,z=10
S3   move P,tg=po1,spd=10%,accu=0,tool=0
     end
```