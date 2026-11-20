# _spot_gun 변수

### 설명

스폿 건별 마모량과 용접 완료 타점 수를 읽거나 변경하는 시스템 변수입니다. <br>
건번호는 1부터 시작합니다.

|멤버|의미|접근|
|:--|:--|:--|
|`fixed_tip_consump`|고정전극 마모량|읽기·쓰기|
|`moving_tip_consump`|이동전극 마모량|읽기·쓰기|
|`total_tip_consump`|고정전극 마모량과 이동전극 마모량의 합|읽기 전용|
|`weld_count`|해당 건의 용접 완료 타점 수 <br> (V70.04-03 이상에서 지원)|읽기·쓰기|

### 문법

```python
     var wear=_spot_gun[1].fixed_tip_consump
     var total_wear=_spot_gun[1].total_tip_consump
     var count=_spot_gun[1].weld_count
     _spot_gun[1].weld_count=0
```

### weld_count의 동작

- 해당 건의 용접 완료가 판정되면 1 증가합니다. 팁드레싱과 서보건 자동 설정 동작은 계산하지 않습니다.
- 사이클 시작 시 모든 건의 카운터가 0으로 초기화됩니다.
- 전원 재투입 시 저장된 값이 복원되며, 전원 복구만으로 초기화하지 않습니다.

