# 4.1.5 배열에 다른 배열을 합치는 프로시져 extend_arr


{% hint style="info" %}

* V60.05-06부터 지원됩니다.

{% endhint %}

배열에 다른 배열을 합쳐 주기 위해 `extend_arr` 프로시져를 사용할 수 있습니다.

```python
var arr = [1, 2]
var brr = [3, 4]
extend_arr arr, brr
print arr   # [1, 2, 3, 4]
```

다음과 같은 방식도 가능 합니다.

```python
var arr = [1, 2]
extend_arr arr, [3, 4, 5]
print arr   # [1, 2, 3, 4, 5]
```
