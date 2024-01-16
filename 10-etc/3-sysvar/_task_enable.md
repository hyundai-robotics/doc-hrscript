# _task.enable 변수

### 설명

서브 태스크가 활성화 된 상태인지 확인하기 위한 시스템 변수입니다.


### 문법

```python
var res
res = _task[1].enable
```


### 사용 예

```python
   ...
   if _task[1].enable==1  #서브태스크 1이 활성화 상태이면
   print "서브태스크 1 활성화 상태임"
   endif
   ...
   end
```


