# 2.3.1 程序

一个程序由一个命令和 0-N 个参数组成。

```python
move P,po3,spd=80%,accu=1,tool=3 until do33
```

三种类型的程序参数如下所示：

| 类型 | 语法 | 示例 |
| :--- | :--- | :--- |
| 位置参数 | &lt;value&gt; | P, po3 |
| 关键字参数 | &lt;keyword&gt; = &lt;value&gt; | spd=80%, accu=1, tool=3 |
| 介词参数 | &lt;preposition&gt; &lt;value&gt; | until do33 |

位置参数的角色由其位置决定，因此不应移动，并且必须始终位于程序的前面。

关键字参数应放在位置参数之后。然而，关键字参数之间的顺序不影响操作。

介词参数应放在最后。