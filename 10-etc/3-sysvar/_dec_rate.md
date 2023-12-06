# _dec_rate 변수

속도 프로파일의 감속도의 비율을 읽거나 설정합니다.

### 설명

단위는 %입니다. 1~100 의 값을 설정할 수 있으며, default값은 100입니다.

### 문법

```python
var res
res = _dec_rate
```

### 사용 예

```python
   ...
   # 현재 감속도 비율 출력한 후, 70%로 설정한다.
   print _dec_rate
   _dec_rate=70
   ...
   end
```
