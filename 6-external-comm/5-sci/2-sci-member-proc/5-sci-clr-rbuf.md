# clr_rbuf

### 설명

Sci의 수신된 버퍼를 초기화 합니다.


### 문법

&lt;Sci객체&gt;.clr_rbuf()

### 리턴값
- 0: 수신 버퍼 초기화 성공
- -1: 실패

### 사용 예

```python
var ret
ret=sci2.clr_rbuf()
if ret<0
  print "receive buffer clear error"
  stop
endif
```



