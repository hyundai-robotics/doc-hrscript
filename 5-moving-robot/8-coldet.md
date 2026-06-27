# 5.8 `coldet`

机器人语言 `coldet` 用于在功能被激活时设置每个轴的碰撞检测级别。

用户应该在 TP 菜单中设置功能的开/关和碰撞级别。 `[F2: 系统] - 3: robot parameter - 14: impact detection - 2: set the collision detection (of each axis) ([F2: System] - 3: robot parameter - 14: impact detection - 2: set the collision detection (of each axis))`

菜单可以在设置为检测碰撞的机器人中显示。

如果功能被激活，默认检测级别为 1。

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
* 步骤 1 和步骤 2 的检测级别值为 1。
* 步骤 3 的检测级别值为 2，步骤 4 和步骤 5 的级别值为 3。
* 在步骤 6 和步骤 7 中，碰撞检测功能被关闭。
---