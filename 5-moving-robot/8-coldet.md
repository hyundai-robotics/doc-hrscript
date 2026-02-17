# 5.8 `coldet`

机器人语言 `coldet` 用于在功能激活时设置每个轴的碰撞检测级别。

用户应在 TP 菜单中设置功能激活开/关和碰撞级别。`[F2: 系统] - 3: 机器人参数 - 14: 碰撞检测 - 2: 设置碰撞检测（每个轴） ([F2: System] - 3: robot parameter - 14: impact detection - 2: set the collision detection (of each axis))`

该菜单可以显示机器人的碰撞检测设置。

如果功能已启动，默认检测级别为 1。

在手动模式下，默认级别也是相同的。

---

### 描述
* 设置碰撞检测级别 


### 语法 
```python
coldet LV=<level> 
```

### 参数 
* 级别的值可以设置为 0 到 16（0: 关闭）

### 示例 

```python
S1   move P,spd=60%,accu=0,tool=0
S2   move P,spd=60%,accu=0,tool=0
     coldet LV=2
S3   move P,spd=60%,accu=0,tool=0
     coldet LV=3
S4   move P,spd=60%,accu=0,tool=0
S5   move P,spd=60%,accu=0,tool=0
     coldet LV=0
S6   move P,spd=60%,accu=0,tool=0
S7   move P,spd=60%,accu=0,tool=0
     end 
```
* 第 1 步和第 2 步中的检测级别值为 1。
* 第 3 步的检测级别值为 2，第 4 步和第 5 步的级别值为 3。
* 在第 6 步和第 7 步中，碰撞检测功能被禁用。 
--- 