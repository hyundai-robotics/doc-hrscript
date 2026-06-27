# 5.15 `convcrd`

### Description 
* `convcrd` 命令是一个功能指令，用于转换姿态变量的坐标系统。

### Syntax 
>* poseA: 要转换的姿态变量。
>* poseB: 转换后的姿态变量。

```python
poseB = poseA.convcrd("base")      # 基准坐标
poseB = poseA.convcrd("robot")     # 机器人坐标
poseB = poseA.convcrd("tool")      # 工具坐标
poseB = poseA.convcrd("u1")        # 用户坐标 1
```

### Example 
```python
     var pose_A, pose_B
     
     # 关节坐标
     pose_A=Pose(0.00,60.00,0.00,0.00,-30.00,0.00)
     # 基准坐标
     pose_B=pose_A.convcrd("base")
```