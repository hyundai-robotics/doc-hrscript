# 7.3.3 `ENet` 成员函数

* 当从成员函数获取返回值时，请确保将参数放在括号中。
  
  ```python
  var nitem=obj.func(param1,param2) # (O) ; 必须使用括号
  var nitem=obj.func param1,param2 # (X) ; 语法错误
  ```

* 可以省略括号，但不获取返回值。

  ```python
  obj.func(param1,param2) # (O)
  obj.func param1,param2 # (O) ; 省略了括号
  ```