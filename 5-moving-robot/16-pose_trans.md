# 5.16 `pose_trans`

### 描述
* `pose_trans` 命令是一个函数指令，用于将两个位姿变量相乘以获得结果位姿值。

### 语法

```python
poseC = pose_trans(poseA,poseB)
```

### 示例
```python
     var pose_A, pose_B, pose_C
     var pose_inv_B
     var pose_shift
     
     pose_shift=Shift(10.0, 10.0, 10.0, 0.000, 0.000, 0.000, "base")

     # pose_A : (0,60,0,0,-30,0) 
     pose_A=Pose(0.00,60.00,0.00,0.00,-30.00,0.00)
     pose_A=pose_A.convcrd("base")
 
     pose_B=pose_A+pose_shift
     
     # pose_inv_B 是 pose_B 的逆矩阵
     pose_inv_B=pose_B
     pose_inv_B=pose_B.convcrd("base")
     pose_inv_B=pose_inv(pose_B)

     # pose_C 与 pose_A 相同
     pose_C=pose_trans(pose_A,pose_B)
     pose_C=pose_trans(pose_C,pose_inv_B)
          
S1   move P,tg=pose_C,spd=10%,accu=0,tool=0
     
     end
```