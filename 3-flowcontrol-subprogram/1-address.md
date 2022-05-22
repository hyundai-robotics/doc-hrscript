# 3.1 Address

Moving to another position in the program without executing the next line in order is called a “branch.”

The address is the destination of the branch.

There are two ways to define an address: line number and label. In the following example, “10” in the second statement is the line number, and the last statement “\*err\_handle” is the label.



```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
10   z_pos = (base_height+offset)*1.05
     # robot has to wait sensor2 input
     *err_handle
```



