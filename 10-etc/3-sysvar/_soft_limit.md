# _soft_limit 변수

소프트 리밋의 값을 읽거나 설정합니다.

### 설명

단위는 직동축은 mm이고 회전축은 deg입니다. 로봇에 지정된 최소 ~ 최대 범위내에서 값을 설정할 수 있습니다.

### 문법

```python
var res
res = _soft_limit[2].min
```

### 사용 예

```python
   ...
   # 1축의 소프트리밋의 최소값을 -90도로 설정한다.
   print _soft_limit[0].min
   _soft_limit[0].min=-90
   ...
   end
```
