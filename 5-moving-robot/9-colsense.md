# 5.9 `colsense` 

机器人语言 `colsense` 用于在功能激活时设置检测灵敏度。

用户应在 TP 菜单中设置功能激活开/关和检测灵敏度。`[F2: 系统] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection ([F2: System] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection)`。

---

### 描述
* 可以设置一般的碰撞检测灵敏度
* 每个轴的碰撞检测灵敏度可以设置

### 语法 
```python
colsense general,sensitivity=<general sensitivity>  
colsense axis,id=<joint number>,criteria=<each axis sensitivity> 
```

### 参数 
* 一般阈值可以设置从 0 到 200，值越大灵敏度越高。(0:0ff,1~200)
* 参数 "id" 设置为关节编号。(1~6)  
* 轴阈值可以设置从 0 到 100，值越低灵敏度越高。(0:0ff,1~100)"

### 示例 

```python
S1   move P,spd=60%,accu=0,tool=0
S2   move P,spd=60%,accu=0,tool=0
     colsense general,sensitivity=150
S3   move P,spd=60%,accu=0,tool=0
     colsense general,sensitivity=200
S4   move P,spd=60%,accu=0,tool=0
S5   move P,spd=60%,accu=0,tool=0
     colsense axis,id=1,criteria=0
     colsense axis,id=2,criteria=0
S6   move P,spd=60%,accu=0,tool=0
S7   move P,spd=60%,accu=0,tool=0
     end 
```
* 第 1 步和第 2 步中的检测灵敏度值基于菜单设置 `[F2: 系统] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection ([F2: System] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection)`。
* 第 3 步中的一般灵敏度为 150，第 4 步和第 5 步时值更改为 200。
* 第 1 关节和第 2 关节的碰撞感应被禁用，其他关节的碰撞根据一般灵敏度 200 被检测。

--- 
{% hint style="info" %}

每个轴的最终灵敏度值与各轴的灵敏度值成正比，与一般灵敏度值成反比。
{% endhint %}