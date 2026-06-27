# `_tool`

`_tool` 是一个系统变量，用于读取或更改工具数据。

### 描述

- 读取注册的工具数据（重量/质心/转动惯量）或更改工具数据。
- 如果工具数据未注册或成员无效，则会发生错误并中断作业执行。

### 语法

```python
<shift variable> = _tool3
_tool3 = <shift>
_tool[3] = <shift>
_tool[5].mass = <arithmetic expression>
_tool[5].cx = <arithmetic expression>
_tool[5].cy = <arithmetic expression>
_tool[5].cz = <arithmetic expression>
_tool[5].ixx = <arithmetic expression>
_tool[5].iyy = <arithmetic expression>
_tool[5].izz = <arithmetic expression>
```

### 错误

- E14550 : 当工具数据的成员无效时发生。确保设置的工具数据的成员是质量、cx、cy、cz、ixx、iyy、izz。
- E14286 : 当赋值语句的右侧不是移位类型或工具变量的成员无效时发生。请正确指定右侧。

### 示例

```python
   var sft=Shift(100,20,30,0,0,0,"tool")
   _tool3=sft
   move L,spd=30%,accu=1,tool=3
   end
```