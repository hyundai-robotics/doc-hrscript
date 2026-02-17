# 10.1.12 `speed_out` 声明

`speed_out` 声明是一个计算与机器人当前运动速度成比例的值并将结果分配给指定变量的过程。  
它仅在执行插值设置为 `左 (L)` 或 `C` 的 `移动 (move)` 声明时起作用。

### 描述

该声明计算与机器人当前移动速度成比例的值，并将计算结果存储在指定变量中。  

如果执行以下命令，如图所示，计算出与当前机器人速度 `x` 相对应的值 `y` 并分配给 dow10。
...  
```python
speed_out on,min_spd=100,max_spd=2000,min_val=10,max_val=100,var=dow10
```

![](../../_assets/speed_out.png)

### 语法
```python
speed_out <on/off>, min_spd=<最低速度>, max_spd=<最高速度>, min_val=<最低值>, max_val=<最高值>, var=<数字变量>
```

### 参数
| 项目    | 描述                                                      | 备注              |
| ------- | ---------------------------------------------------------- | ---------------- |
| on/off  | 指定函数启用的部分                                       |                  |
| min_spd | 指定最低机器人移动速度 [mm/s]                           |                  |
| max_spd | 指定最高机器人移动速度 [mm/s]                           |                  |
| min_val | 指定与最低机器人速度相对应的值                         |                  |
| max_val | 指定与最高机器人速度相对应的值                         |                  |
| var     | 指定存储计算值的变量                                    | 数字变量         |

### 示例

```python
   move P,spd=30%,accu=0,tool=1
   speed_out on,min_spd=100,max_spd=2000,min_val=10,max_val=100,var=dow10
   move L,spd=30mm/s,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   speed_out off
   move P,spd=30%,accu=0,tool=1
   end
```