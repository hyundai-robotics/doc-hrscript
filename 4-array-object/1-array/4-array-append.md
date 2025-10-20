# 4.1.4 배열 원소 추가 프로시져 append_arr

{% hint style="info" %}

* V60.05-06부터 지원됩니다.

{% endhint %}

배열에 원소를 추가 하려면 `append_arr` 프로시져를 사용할 수 있습니다.

```python
var arr = [1, 2]
append_arr arr, 3   # 원소 3을 추가
print arr           # [1, 2, 3]
```

배열의 원소는 타입과 상관없이 사용할 수 있기 때문에 다른 배열을 원소로 추가 할 수 있습니다.

```python
var arr = [1, 2]
append_arr arr, [3, 4]  # 원소 [3, 4]를 추가
print arr               # [1, 2, [3, 4]]
```
