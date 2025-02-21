# close

### 설명

Sci의 close 를 실행하여 시리얼 포트를 닫습니다.


### 문법

&lt;Sci객체&gt;.close()

### 리턴값
- 0: 닫기 성공
- -1: 이미 닫혔음.

### 사용 예

```python
var ret
ret=sci2.close()
if ret<0
  print "open error"
  stop
endif
```



