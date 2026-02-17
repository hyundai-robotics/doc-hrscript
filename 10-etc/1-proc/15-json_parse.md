# 10.1.15 `json_parse`

支持版本：V60.32-00

`json_parse` 过程解析 JSON 字符串以构建对象、数组或值。

### 语法

在过程开始后，`result()` 函数返回一个结果对象，用于检查状态和存储结果数据。
```python
    json_parse <json string literal/value>
    var r = result()
```

您必须等待此过程完成。
```python
    wait r.status == "finished"
```

解析的结果将存储在 `r.data` 中。如果在访问结果之前不允许程序完成，则可能会发生错误。

##### 状态

<table>
  <thread>
    <th style="text-align:left">状态</th>
    <th style="text-align:left">详细信息</th>
  </thread>
  <tbody>
  <tr>
    <td style="text-align:left">解析中</td>
    <td style="text-align:left">JSON 字符串仍在解析中。数据尚不可用。</td>
  </tr>
  <tr>
    <td style="text-align:left">已完成</td>
    <td style="text-align:left">JSON 字符串解析已完成。数据现在可用。</td>
  </tr>
  </tbody>
</table>

### 示例
```python
    json_parse "[1, 2, 3, 4]"
    var r = result()
    wait r.status == "finished", 10 # 等待进程完成，最长超时 10 秒。
    var jr = r.data   # r.data 的类型是数组
    print jr          # 打印 [1, 2, 3, 4]
```
    json_parse "3.141592"
    var r = result()
    wait r.status == "finished", 10 # 等待进程完成，最大超时为10秒。
    var jr = r.data    # r.data 的类型为 double
    print jr           # 打印出 3.141592
```
```python
    json_parse "{\"test\": \"value\"}" # JSON 字符串内部的双引号必须被转义。
    var r = result()
    wait r.status == "finished", 10 # 等待进程完成，最大超时为10秒。
    var jr = r.data    # r.data 的类型为 JObject
    print jr           # 打印出 { _type: "JObject", _sub_file: "", _desc: "", test: "value" } 
```