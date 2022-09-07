# 7.3.3 ENet 멤버 함수

* 멤버 함수는 리턴값을 받을 때는 반드시 인수를 괄호로 묶어주십시오.  
  
  ```python
  var nitem=obj.func(param1,param2) # (O) ; 괄호 필수
  var nitem=enet.recv bbuf,5000,*TimeOut # (X) ; 문법 오류
  ```

* 리턴값을 받지 않을 때는 괄호를 생략할 수 있습니다.  

  ```python
  obj.func(param1,param2) # (O)
  obj.func param1,param2 # (O) ; 괄호 생략
  ```