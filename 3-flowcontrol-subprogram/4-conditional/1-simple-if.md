# 3.4.1 单行 `if`

### 描述

单行 `if` 语句的形式如下：如果 &lt;布尔表达式&gt; 为真，将分支到 &lt;地址&gt;。如果为假，则移动到下一个语句。

### 语法

```python
if <bool expression> then <address>
```

### 示例

下面是单行 if 语句的示例。如果压力大于限制的条件为真，则将分支到标签地址 "\*err"，使得可以打印出压力过高的警告。如果条件为假，则下一个语句将一个接一个地执行，而不会分支，因此将打印 "正常运行中" 并结束程序。

```python
var pressure=95, limit=90
if pressure > limit then *err
print "in normal operation."
end
*err
print "warning: pressure is too high."
```