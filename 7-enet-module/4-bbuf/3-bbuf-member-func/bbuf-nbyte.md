# nbyte

### 문법

{BBuf객체}.nbyte


### 리턴값

바이터리 데이터의 크기 (byte수)


### 사용 예

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
print bbuf.nbyte() # "8"
```

