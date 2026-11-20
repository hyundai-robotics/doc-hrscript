# _spot_cnd 변수

### 설명

스폿 용접조건별 클리어런스 값을 읽거나 변경하는 시스템 변수입니다. <br>
조건번호는 1부터 시작합니다.

|멤버|의미|접근|
|:--|:--|:--|
|`fixed_tip_clearance`|고정전극 클리어런스|읽기·쓰기|
|`moving_tip_clearance`|이동전극 클리어런스|읽기·쓰기|

### 문법 및 사용 예

```python
     var clearance=_spot_cnd[1].fixed_tip_clearance
     _spot_cnd[1].fixed_tip_clearance=clearance
```

