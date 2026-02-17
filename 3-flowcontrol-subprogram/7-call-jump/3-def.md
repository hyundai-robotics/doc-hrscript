# 3.7.3 `def` (定义用户函数)

since V60.05-06

### 描述

您可以在作业中使用 `def` 语句定义用户函数，并使用 `call` 语句调用它。与 `param` 语句类似，`def` 语句可以指定形式参数的列表。`call` 语句的实际参数值会传递给形式参数。使用 `def` 语句定义的函数执行完后，会在 `call` 语句的下一个语句处返回，当执行 `return` 语句或 `end` 语句时。

用户函数是通过名称调用而不是编号，因此其可读性优于子程序。您可以将多个相关函数分组到一个子程序中，以改善项目结构。

### 语法

```python
def <用户函数名称> [,parameter1[=默认值],parameter2[=默认值],...]
```

在 `def` 后指定用户函数名称。函数名称必须遵循第 [2.2 标识符](../../2-basic-syntax/2-identifier.md) 节中定义的规则。此外，它应该是全局唯一的名称。注意不要与其他函数名称或变量名称重复新的名称。
之后，指定形式参数。您还可以为每个参数指定默认值。如果在 `call` 语句中省略了实际参数，形式参数将被初始化为默认值。如果您开始为特定形式参数指定默认值，则必须为最后一个参数之前的所有参数指定默认值。

```python
# 默认值的形式参数示例
def set_work,mass,cx=0,cy=0,cz=0 # 合法示例
def set_work,mass,cx=0,cy,cz     # 非法示例
```

### 示例

以下是带有 `call` 语句的用户函数调用示例及其结果。我们在前一节中介绍了欧几里得距离的示例以描述子程序。现在，让我们分别定义欧几里得距离和曼哈顿距离的用户函数，并调用它们。

```python
# 0001_main.job
var x,y
x=5
y=12.8

call euclid_dist,x,y
var res=result()
print "euclid=",res # 13.7419

call manhattan_dist,x,y
var res=result()
print "manhattan=",res # 17.8
end
```

```python
# 0008_dist.job

# 计算 2D 欧几里得距离
def euclid_dist,x,y
var tmp
tmp=x*x+y*y
var len=sqr(tmp) # 从原点的距离
return len

# 计算 2D 曼哈顿距离
def manhattan_dist,x,y
var len=x+y
return len
```
<br>

RESULT
```python
euclid= 13.7419
manhattan= 17.8
end
```