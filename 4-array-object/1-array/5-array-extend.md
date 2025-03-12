# 4.1.5 배열에 다른 배열을 합치는 프로시져 extend

V60.32-01 부터 지원 예정입니다.

배열에 다른 배열을 합쳐 주기 위해 extend 프로시져를 사용할 수 있습니다.

```python
var arr = [1, 2]
var brr = [3, 4]
extend arr, brr
print arr   # [1, 2, 3, 4]
```

다음과 같이 임시 배열도 사용 가능 합니다.

```python
var arr = [1, 2]
extend arr, [3, 4, 5]
print arr   # [1, 2, 3, 4, 5]
```
