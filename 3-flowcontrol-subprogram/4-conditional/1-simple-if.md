# 3.4.1 单行 `如果 (if)`

### 描述

单行 `如果 (if)` 语句的形式如下：如果 &lt;布尔表达式&gt; 为真，则将发生跳转到 &lt;地址&gt;。如果为假，则将移动到下一个语句。

### 语法

```python
if <bool expression> then <address>
```

### 示例

以下是单行 if 语句的示例。如果压力大于限制的条件为真，则将发生跳转到标签地址 "\*err"，从而可以打印出压力过高的警告。如果条件为假，则将一个接一个地执行下一个语句，因此将打印 "正常运行中 "，结束程序。

```python
var pressure=95, limit=90
if pressure > limit then *err
print "normal operation."
end
*err
print "warning: pressure is too high."
```