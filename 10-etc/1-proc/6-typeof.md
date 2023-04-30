# 10.1.6 typeof문

typeof문은 변수나 식의 타입을 확인하는 프로시져입니다. 결과는 result() 함수로 리턴받습니다.

### 문법

```python
typeof <식>
```


### 사용 예

```python
     global done=true,msg="Timeout Error"
     var a=-2000, b=3.14
     var myarr=[1,2,3]
     var myobj={x:30, y:"off"}
     var po=Pose(0,90,0,0,0,0)

     typeof done
     print result() # "bool" 
     typeof msg
     print result() # "string"
     typeof a
     print result() # "int"
     typeof b
     print result() # "double"
     typeof myarr
     print result() # "array"
     typeof myobj
     print result() # "object"
     typeof po
     print result() # "object"
     end
```
