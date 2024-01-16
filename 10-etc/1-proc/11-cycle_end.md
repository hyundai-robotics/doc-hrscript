# 10.1.11 cycle_end문

cycle_end문은 call문의 수행에 의해 관리되던 호출 스텍을 모두 클리어하는 프로시져입니다.

### 설명

프로그램 end문을 수행할 때 호출 스텍이 존재하는 경우 call문을 수행한 위치로 되돌가 가서 프로그램 실행을 계속 수행합니다. <br>
그런데 cycle_end문을 실행하면 관리되던 호출 스텍이 모두 클리어되어 call문을 수행한 위치로 되돌아 가지않고 정지합니다. <br>

### 문법

```python
cycle_end 
```


### 사용 예

```python
   0001.job
   ...
   move P,spd=30%,accu=0,tool=1
   call 10
   move P,spd=30%,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   move L,spd=30mm/s,accu=0,tool=1
   delay 0.5
   move P,spd=30%,accu=0,tool=1
   end


   0010.job
   ...
   move P,spd=30%,accu=0,tool=1
   delay 0.5
   cycle_end


```
