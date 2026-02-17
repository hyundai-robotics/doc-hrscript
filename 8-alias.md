# 8. 别名

别名是可以作为变量或对象属性表示法的替代名称。

别名是可以用来表示变量或对象的替代名称。您可以使用简洁的名称替换过长的属性表示法，或用更易读的名称替换特定索引的IO变量。

别名通过 `alias` 语句定义，语法几乎与 `var` 或 `global` 相同。

别名的作用域与全局相同。也就是说，在执行 `alias` 语句后，它可以在任何后续作业中使用，即使主程序通过 `end` 语句或 `R0 - [ENTER]` 操作重置程序周期，别名也不会被销毁。

```python
global myval=3, yourname="Jane"
val i=0,msg="hello"
val profile = { name: "Paul", age: 43, role: [ "CTO", "engineer" ] }

alias grip=fb3.do4, work_no=fb1.diw2 # (1)
alias role=profile.role # (2)
alias tool0=project.robot.tools.t_0 # (3)

# 使用
grip=1
print work_no
print role[1]
tool0.mass=12
```

在上面的例子中，(1) 的输出变量 `fb3.do4` 被定义为名为 `grip` 的别名，而输入变量 `fb1.diw2` 被定义为别名 `work_no`。  
在 (2) 中，作为 `profile` 属性的角色数组被定义为别名 `role`。  
在 (3) 中，内置对象 `project.robot.tools.t_0` 被定义为别名 `tool0`，指向工具数据 \#0。

对于引用数组的别名，其元素可以用 [ ] 操作符指定，如 `role[1]`。  
对于引用对象的别名，其属性可以用 . 操作符指定，如 `tool0.mass`。

常量不能定义为别名。使用 `global` 或 `var` 定义它。  
表达式也不能定义为别名。请注意，这可能导致故障。

```python
#alias pie=3.141592 # (X)
#alias unit="mm/s" # (X)
global pie=3.141592 # (O)
global unit="mm/s" # (O)

#alias pie_2 = pie*pie # (X)
```