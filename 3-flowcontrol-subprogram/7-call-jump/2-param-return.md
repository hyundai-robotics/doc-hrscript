# 3.7.2 参数和 `param`， `return`

在作业程序中，正式参数作为输入和输出传递的通道。 `param` 语句将在作业程序的开头定义正式参数。

在以下示例中，作业编号 105 被命名为 "dist2d"，因为它是一个子作业，获取从原点到坐标值 \(x, y\) 的欧几里得距离并将其返回到 len。

```python
# 0001_main.job
var x,y
x=5
y=12.8
call 105_dist2d,x,y
var res=result()
print res
end
```

```python
# 0105_dist2d.job
# 计算二维欧几里得距离
param dx,dy
var tmp

tmp=x*x+y*y
var len=sqr(tmp) # 从原点的距离
return len
```

<br>

结果
```python
13.742
```

在作业编号 1 中，dist2d 子程序通过 `call` 语句被调用，"x, y," 作为局部变量被传递。在 dist2d 子程序中，通过 `param` 语句定义的 "dx" 和 "dy" 被称为 "正式参数"，而传递给 `call` 语句的 "x, y" 被称为 "实际参数"。

dist2d 程序通过 `return` 语句将结果值传输到外部目的地。返回的值可以通过在被调用程序中调用 result\(\) 函数来获取。

(`return` 语句和 `end` 语句具有相同的作用，因为它们结束被调用程序并返回到主程序。然而，`return` 语句与 `end` 语句不同，因为前者可以将结果值指定为元素)。