# 5.3 포즈식 \(pose expression\)

결과값이 포즈가 되는 수식을 포즈식이라고 합니다.

아래와 같은 형태가 모두 포즈식으로 인식됩니다.



```python
포즈
포즈+시프트
포즈-시프트
포즈+시프트+시프트+…
```

포즈식의 결과를 다른 포즈 변수에 대입하는 아래의 예를 참고하십시오.

```python
var po1 = Pose(10, 90, 0, 0, -30, 0)
var po2 = Pose(1850, 0, 2010.5, 0, -90, 0, "base", "fl;r2")
var po3 = cpo("robot")
var sft1 = Shift(30, 0, 0, 0, -5.8, 0)
var po4 = po1-sft1
var po5 = po2+sft1+Shift(0, 0, 55.2, 0, -5, 0, "base")
```

