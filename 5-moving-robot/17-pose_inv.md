# 5.17 pose_inv 문


## 설명 
* pose_inv 명령어는 해당 포즈 변수의 역행렬에 해당하는 포즈 변수로 변환하는 함수 명령어 이다.  


## 문법 
>* 포즈변수(poseB)는 포즈변수(poseA)의 역행렬에 해당하는 포즈 변수이다.    
>* 포즈 변수(poseA)를 4x4 transformation 행렬로 변환하고, 이 행렬값의 역행렬을 계산한 뒤 다시 포즈 변수(PoseB)로 변환 하는 방식이다.  
```python
poseB = pose_inv(poseA)
```

## 사용 예  
```python
     var pose_A, pose_B, pose_C
     var pose_inv_B
     var pose_shift
     
     pose_shift=Shift(10.0, 10.0, 10.0, 0.000, 0.000, 0.000, "base")

     # pose_A는 축각도 (0,60,0,0,-30,0)의 자세 
     pose_A=Pose(0.00,60.00,0.00,0.00,-30.00,0.00)
     pose_A=pose_A.convcrd("base")

     # pose_B는 pose_A자세에서 base좌표계 기준 XYZ 방향으로 10mm씩 이동 
     pose_B=pose_A+pose_shift
     
     # pose_B의 inverse matrix를 뜻하는 pose_inv_B 구하기 
     pose_inv_B=pose_B
     pose_inv_B=pose_B.convcrd("base")
     pose_inv_B=pose_inv(pose_B)

     # pose_C는 pose_A*pose_B*pose_inv_B의 결과 값으로, 결국 pose_A와 동일해야 한다. 
     pose_C=pose_trans(pose_A,pose_B)
     pose_C=pose_trans(pose_C,pose_inv_B)
          
     # pose_C를 목표 지점으로 설정하면, pose_A에서 설정한 축각도 (0,60,0,0,-30,0)의 자세로 이동한다. 
S1   move P,tg=pose_C,spd=10%,accu=0,tool=0
     
     end
```


