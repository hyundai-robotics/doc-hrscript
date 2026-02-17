# 3.7.1 `call`

### 描述

HRScript中主程序和子程序的格式没有显著区别。通过启动按钮或信号执行的第一个任务是主程序，所有通过`call`语句调用的其他任务则是子程序。

### 语法

```python
call <作业编号，文件名或用户函数名> [,参数1,参数2,...]
```

在`call`语句后指定作业文件名的作业编号（不包括扩展名）。然后，在执行程序`A`时，如果遇到调用`B`，将停止执行`A`，并继续执行子程序`B`的第一条语句。如果在执行`B`时遇到`end`或`return`语句，程序`A`的执行将在返回到之前调用的程序`A`的`call`语句的下一条语句的位置继续。

### 示例

以下显示了通过`call`语句调用的子程序的示例及结果。将程序分成两个似乎没有意义，因为子程序必须仅处理一个打印语句。不过，将在后面展示一个更实用的例子。

* 请参见[3.7.3 def](./3-def.md)以获取调用用户函数的示例。

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

结果
```python
main job start
sub-program
main job end
```