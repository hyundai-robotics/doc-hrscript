# 3.7.4 `jump`

### 描述

此格式与 `call` 语句完全相同，其动作也与 `call` 语句类似。

唯一的区别是，`call` 语句使用 `end` 语句返回到主程序，而 `jump` 语句则不这样做。

### 语法

```python
jump <作业编号或文件名称> [,参数 1,参数 2,???]
```

### 示例

如果将此示例程序的 `jump` 语句替换为 `call` 语句，则替换后的程序结果如下。当遇到子程序 \(0102\_err\) 的 `end` 时，动作循环将结束。如果执行下一个动作循环，主程序 \(0001\) 将从头开始执行。

```python
# 0001_main.job
print "main job start"
jump 102_err
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
```