# `_vel_rpm_cmd`

读取或设置电机在控制额外轴时旋转的速度。

### Description

额外轴必须在夹具轴上设置为速度控制模式。<br>
单位是 rpm。您可以设置一个介于 -10000 和 10000 之间的值，默认值为 0。<br>
如果指定为 -，电机将反向旋转。

### Syntax

```python
var res
_vel_rpm_cmd[6] = 1000 # 以 1000 rpm 的速度旋转 7 轴电机 
res = _vel_rpm_cmd[6] # 赋值 7 轴电机的旋转速度 
```

### Sample

```python
   ...
   # 打印当前 7 轴电机旋转速度后，将其设置为 1000 rpm。
   print _vel_rpm_cmd[6]
   _vel_rpm_cmd[6]=1000
   ...
   end
```