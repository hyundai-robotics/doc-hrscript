# 6.6.1 构造函数

### 描述

为 `RSI` 对象创建一个全局变量。

### 语法

com.RSI(enet 对象) <br>

指定用于以太网通信设置的对象。例如，如果使用的对象名称是 "enet0"，则指定 _enet0；如果是 "enet1"，则指定 _enet1。  

### 返回值

创建对象的引用

### 示例

```python
global rsi
rsi=com.RSI(_enet0)  # _enet0 在以太网通信设置中使用 "enet0" 对象 
```