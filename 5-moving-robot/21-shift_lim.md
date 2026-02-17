# 5.21 `shift_lim`

`shift_lim`语句是一个函数，通过设置机器人最大允许偏移量来提高使用偏移功能的安全性。  
如果输入的偏移值超过配置的限制，将产生错误。

### 语法
```python
shift_lim x=<X 偏移限制>, y=<Y 偏移限制>, z=<Z 偏移限制>
```

### 参数
* x, y, z: X, Y, Z 偏移限制值[0~3000,mm]<br><br>

### 错误指南
* E1196: 偏移量超过配置的偏移限制。请减少偏移量或重新调整偏移限制值。

### 示例
```python
     var po1 = Pose(0.691, 99.293, 24.758, -6.528, -48.574, 15.774, 0.000)
S1   move P, tg=po1, spd=10%, accu=0, tool=0
     shift_lim x=120, x=200, z=100
     shift crd="base", x=-150, y=70, z=10  # 偏移限制超出错误发生
S2   move P, tg=po1, spd=10%, accu=0, tool=0
     end
```