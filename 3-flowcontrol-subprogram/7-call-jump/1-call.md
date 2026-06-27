# 3.7.1 `call`

### 描述

在 HRScript 中，主程序和子程序之间在格式上没有显著区别。通过启动按钮或信号执行的第一个作业是主程序，所有通过 `call` 语句调用的其他作业都是子程序。

### 语法

```python
call <作业编号, 文件名, 或用户函数名> [,参数 1,参数 2,...]
```

在 `call` 语句之后指定作业文件名的作业编号（不包括扩展名）。然后，当程序 ` (A)` 正在执行时，如果遇到 `call (B)`，将停止执行 ` (A)`，并继续执行子程序 ` (B)` 的第一条语句。如果在执行 ` (B)` 时遇到 `end` 或 `return` 语句，程序 ` (A)` 将在返回到之前调用的程序 ` (A)` 的 `call` 语句的下一条语句的位置继续执行。

### 示例

以下显示了通过 `call` 语句调用的子程序的示例及结果。将程序划分为两个部分似乎毫无意义，因为子程序必须处理仅一个打印语句。然而，稍后将显示一个更实际的示例。

* 请参阅 [3.7.3 def](./3-def.md) 以获取调用用户函数的示例。

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