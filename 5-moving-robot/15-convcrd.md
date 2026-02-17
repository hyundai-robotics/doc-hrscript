# 5.15 `convcrd`

### 描述 
* `convcrd` 命令是一个函数指令，用于转换姿态变量的坐标系统。

### 语法 
>* poseA: 要转换的姿态变量。
>* poseB: 转换后的姿态变量。

```python
poseB = poseA.convcrd("base")      # base coordinate
poseB = poseA.convcrd("robot")     # robot coordinate
poseB = poseA.convcrd("tool")      # tool coordinate
poseB = poseA.convcrd("u1")        # user coordinate 1
```

### 示例 
```python
     var pose_A, pose_B
     
     # 关节坐标
     pose_A=Pose(0.00,60.00,0.00,0.00,-30.00,0.00)
     # 基坐标
     pose_B=pose_A.convcrd("base")
```