# 2.1 Statements

The statement refers to each command string that becomes the execution unit of the job program. HRScript allows only one statement per line. Take note of how the four examples of statements are written below, particularly their appearances.

```python
     move P,po3,spd=80%,accu=1,tool=3 until do33
10   z_pos = (base_height+offset)*1.05
     # robot has to wait sensor2 input
     *err_handle
```

For statements other than a step statement \(move statements, etc.\) that moves the robot, you can optionally add a line number \(1 to 9999\) at the beginning of the line. The number 10 in the second line is an example of a line number.

It does not matter if there are any number of spaces or tabs before and after the statement.

Proper indentation in statements is recommended for readability. Both spaces and tabs are allowed for indentation and do not affect the operation during execution.





