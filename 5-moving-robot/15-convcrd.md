# 5.15 convcrd


### Description 
* convcrd command is a function instruction that converts the coordinate system of the pose variable.


### Syntax 
>* poseA: The pose variable to be converted.
>* poseB: Converted pose variable.

```python
poseB = poseA.convcrd("base")      # base coordinate
poseB = poseA.convcrd("robot")     # robot coordinate
poseB = poseA.convcrd("tool")      # tool coordinate
poseB = poseA.convcrd("u1")        # user coordinate 1
```

### Example 
```python
     var pose_A, pose_B
     
     # joint coordinate
     pose_A=Pose(0.00,60.00,0.00,0.00,-30.00,0.00)
     # base coordinate
     pose_B=pose_A.convcrd("base")
```


