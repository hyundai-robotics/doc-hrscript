# 5.15 convcrd 문


## 설명 
* convcrd 명령어는 포즈 변수의 좌표계를 변환하는 함수 명령어입니다.  


## 문법 
>* 포즈 변수(poseA)는 변환할 포즈변수, 포즈변수(poseB)는 변환된 포즈변수입니다.

```python
poseB = poseA.convcrd("base")      #베이스 좌표계
poseB = poseA.convcrd("robot")     #로봇 좌표계
poseB = poseA.convcrd("tool")      #툴 좌표계
poseB = poseA.convcrd("u1")        #1번 사용자 좌표계 
```

## 사용 예  
```python
     var pose_A, pose_B
     
     # pose_A는 축각도 (0,60,0,0,-30,0)의 자세 
     pose_A=Pose(0.00,60.00,0.00,0.00,-30.00,0.00)
     pose_B=pose_A.convcrd("base")
```

