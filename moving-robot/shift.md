# 5.2 시프트 \(shift\)

시프트는 hi6 제어기에 기본 내장된 객체형으로서, 포즈에 대한 변경값을 표현합니다.

시프트는 생성자 함수 Shift\( \)를 호출하여 생성합니다. 함수 매개변수들은 모두 위치 매개변수입니다. crd와 cfg는 문자열형이고, 나머지는 모두 숫자형입니다.

```python
var 시프트변수명 = Shift(j1, j2, j3, …)				# 축 좌표
var 시프트변수명 = Shift(x, y, z, rx, ry, rz, j7, j8,…, crd)		# base 좌표
```

6축+부가1축, 직교+부가 1축의 시프트를 생성하는 아래의 예를 참고하십시오.

```python
var sft1 = Shift(30, 0, 0, 0, -5.8, 0, -120)				# 축 좌표
var sft2 = Shift(0, 0, 55.2, 0, -5, 0, -120, "base")			# base 좌표
```

혹은, 1개의 배열 혹은 문자열 매개변수로도 Shift 생성자 함수를 호출할 수 있습니다. 이를 활용해, 파일이나 원격통신으로 얻은 데이터를 시프트로 변환해 사용할 수 있습니다.

```python
var 시프트변수명 = Shift(array)
var 시프트변수명 = Shift(string)
```

아래의 예를 참고하십시오.

```python
var arr = [30, 0, 0, 0, -5.8, 0, -120]
var str = "[0, 0, 55.2, 0, -5, 0, -120, \"base\"]"
var sft3 = Shift(arr)
var sft4 = Shift(str)
```

Shift 객체의 요소들은 다음의 키들로 접근 가능합니다.

![](../.gitbook/assets/image%20%284%29.png)

