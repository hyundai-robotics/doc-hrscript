# 3.7.1 call문

### 설명

HRScript에서 메인 프로그램\(main program\)과 서브 프로그램\(sub program\) 간의 형식 상의 큰 차이는 없습니다. 기동 버튼이나 신호로 처음 실행된 JOB은 주 프로그램이고, call 명령문에 의해 호출된 JOB은 모두 서브 프로그램입니다. 

### 문법

```python
call <JOB번호 혹은 파일이름, 사용자함수명> [,매개변수1,매개변수2,…]
```

call 뒤에 JOB 번호, 혹은 JOB파일이름\(확장자 제외\)이나 사용자함수명을 지정합니다. A라는 프로그램이 수행되다가 call B를 만나면 A의 수행은 중단되고, 서브프로그램인 B 프로그램(혹은 사용자함수)의 첫 명령문부터 수행이 계속됩니다. B 수행 중 end문이나 return 문을 만나면 호출했던 A 프로그램 call문의 다음 명령문 위치로 복귀하여 A의 수행을 계속하게 됩니다.

### 사용 예

아래는 call 문에 의한 서브프로그램 호출의 예와 그 결과입니다. 서브프로그램이 하는 일이 print문 1개 뿐이라 프로그램을 둘로 분리한 것이 의미없어 보이기는 하지만 뒤에서 좀 더 실제적인 예를 보이도록 하겠습니다.

* 사용자 함수를 호출하는 예는 [3.7.3 def](./3-def.md)를 참조하십시오.

<br>

```python
# 0001_main.job
print "main job start"
call 102_err
print "main job end"
end
```

```python
# 0102_err.job
print "sub-program"
end
```

<br>
결과

```python
main job start
sub-program
main job end
```
