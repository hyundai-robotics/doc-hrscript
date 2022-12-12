# 7.3.3 ENet member function

* When getting the return value from a member function, be sure to enclose the argument in parentheses.
  
  ```python
  var nitem=obj.func(param1,param2) # (O) ; parentheses is necessary
  var nitem=obj.func param1,param2 # (X) ; syntax error
  ```

* Parentheses can be omitted, not getting the return value.

  ```python
  obj.func(param1,param2) # (O)
  obj.func param1,param2 # (O) ; parentheses omitted
  ```