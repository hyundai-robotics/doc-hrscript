# 2.5.1 字符串数据类型

上一段中的第一个程序使用数据 "Hello, World!" 作为打印语句的参数，即字符串数据类型。字符串数据类型的值以双引号开始和结束。字符串的长度没有限制。

```python
print "Welcome to the Robot World."
```

以反斜杠 \(\\) 开头的序列表示字符串中的双引号或特殊字符。这个序列称为“转义字符”。

支持的转义字符如下面的表格所示。



|  |  |
| :--- | :--- |
| \" | 双引号 |
| \\ | 反斜杠 |
| \t | 制表符 |
| \n | 换行符 |

```python
print "Message:\nPlease, press \"OK\" button."

# Result of print
Message:
Please, press "OK" button.
```