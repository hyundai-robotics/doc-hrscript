# `open`

### 描述

执行 `Sci` 的 `open()` 函数以打开串口。

串口通过控制器设置以预设内容打开，无需单独打开端口，除非端口之前已关闭。（默认：打开）


### 语法

&lt;Sci 对象&gt;.open()

### 返回值
- 0: 成功
- <0: 失败


### 示例

```python
var ret
ret=sci2.open()
if ret<0
  print "open error"
  stop
endif
```