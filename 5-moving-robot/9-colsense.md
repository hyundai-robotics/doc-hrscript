# 5.9 `colsense` 

机器人语言 `colsense` 用于在功能激活时设置检测灵敏度。

用户应在 TP 菜单中设置功能激活开关和检测灵敏度。`[F2: 系统] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection ([F2: System] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection)`。

---

### 描述
* 可以设置一般碰撞检测灵敏度
* 可以设置每个轴的碰撞检测灵敏度

### 语法 
```python
colsense general,sensitivity=<一般灵敏度>  
colsense axis,id=<关节编号>,criteria=<每个轴灵敏度> 
```

### 参数 
* 一般阈值范围从 0 到 200，值越大灵敏度越高。(0:0ff,1~200)
* 参数 "id" 设置为关节编号。(1~6)  
* 轴阈值范围从 0 到 100，值越小灵敏度越高。(0:0ff,1~100)"

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
* 步骤 1 和步骤 2 的检测灵敏度值来自于菜单 `[F2: 系统] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection ([F2: System] - 3: robot parameter - 14: impact detection - 1: Model-based collision detection)` 中的设置。
* 步骤 3 中的一般灵敏度为 150，在步骤 4 和步骤 5 中更改为 200 
* 关节 1 和关节 2 上的碰撞检测已被停用，其他关节的碰撞通过一般灵敏度 200 进行检测。  

--- 
{% hint style="info" %}

每个轴的最终灵敏度值与每个轴的灵敏度值成正比，与一般灵敏度值成反比。 
{% endhint %}
