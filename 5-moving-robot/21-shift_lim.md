# 5.21 `shift_lim`

`shift_lim` 语句是一个通过设置机器人可允许的最大移动量来提高使用移动功能时安全性的函数。  
如果输入的移动值超过配置的限制，将产生错误。

### 语法
```python
shift_lim x=<X 移动限制>, y=<Y 移动限制>, z=<Z 移动限制>
```

### 参数
* x, y, z: X, Y, Z 移动限制值[0~3000,mm]<br><br>

### 错误指南
* E1196: 移动量超过配置的移动限制。减少移动量或重新调整移动限制值。

### 示例
```python
     var po1 = Pose(0.691, 99.293, 24.758, -6.528, -48.574, 15.774, 0.000)
S1   move P, tg=po1, spd=10%, accu=0, tool=0
     shift_lim x=120, x=200, z=100
     shift crd="base", x=-150, y=70, z=10  # 超过移动限制的错误发生
S2   move P, tg=po1, spd=10%, accu=0, tool=0
     end
```