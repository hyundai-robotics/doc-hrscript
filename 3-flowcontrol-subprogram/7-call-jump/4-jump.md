# 3.7.3 jump문

### 설명

jump 문의 형식은 아래와 같습니다. 

### 문법

```python
jump <JOB번호 혹은 파일이름> [,매개변수1,매개변수2,…]
```

형식이 call문과 완전히 동일하며 동작도 유사합니다.

유일한 차이점은 call 문은 end문에 의해서 주 프로그램으로 리턴하지만, jump문은 리턴하지 않는다는 점입니다.

### 사용 예

call문 설명에서 본 예제 프로그램을 jump문으로 바꾸어 실행해 보면 결과는 아래와 같습니다. 서브프로그램\(0102\_err\)의 end를 만났을 때, 동작 사이클이 종료됩니다. 다음 동작 사이클을 수행하면, 주 프로그램\(0001\)의 처음부터 수행됩니다.


```python
# 0001_main.job
print "main job start"
jump 102_err
print "main job end"
end
```

```python
# 0102_err.job
print "sub-program"
end
```

결과
```python
main job start
sub-program
```
