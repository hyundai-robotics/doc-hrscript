# clear

### 설명

바이너리 버퍼에 저장된 데이터를 전부 삭제합니다.


### 문법

`{BBuf객체}.clear()`


### 리턴값

없음


### 사용 예

```python
var bbuf=enet.BBuf()
bbuf.append("s4", 20)
bbuf.append("s4", -10)
bbuf.clear()
```
