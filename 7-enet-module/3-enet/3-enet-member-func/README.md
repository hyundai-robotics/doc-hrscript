# 7.3.3 `ENet` 成员函数

* 当从成员函数获取返回值时，请确保将参数用括号括起来。
  
  ```python
  var nitem=obj.func(param1,param2) # (O) ; 括号是必需的
  var nitem=obj.func param1,param2 # (X) ; 语法错误
  ```

* 可以省略括号，未获取返回值。

  ```python
  obj.func(param1,param2) # (O)
  obj.func param1,param2 # (O) ; 括号省略
  ```