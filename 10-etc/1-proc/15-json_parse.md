# 10.1.15 `json_parse`

Supported from V60.32-00

The `json_parse` procedure parses a JSON string to build an object, an array, or a value.

### Syntax

Right after the procedure starts, the `result()` function returns a result object used for checking the status and storing the result data.
```python
    json_parse <json string literal/value>
    var r = result()
```

You must wait for this procedure to complete.
```python
    wait r.status == "finished"
```

The result of parsing will be stored in `r.data`. An error may occur if the procedure is not allowed to finish before accessing the result.


##### status

<table>
  <thread>
    <th style="text-align:left">status</th>
    <th style="text-align:left">details</th>
  </thread>
  <tbody>
  <tr>
    <td style="text-align:left">parsing</td>
    <td style="text-align:left">JSON 字符串仍在被解析中。数据尚不可用。</td>
  </tr>
  <tr>
    <td style="text-align:left">finished</td>
    <td style="text-align:left">JSON 字符串解析完成。数据现在可以使用。</td>
  </tr>
  </tbody>
</table>



### Examples
```python
    json_parse "[1, 2, 3, 4]"
    var r = result()
    wait r.status == "finished", 10 # 等待进程完成，最大超时为 10 秒。
    var jr = r.data   # r.data 的类型为 array
    print jr          # [1, 2, 3, 4] 打印
```

```python
    json_parse "3.141592"
    var r = result()
    wait r.status == "finished", 10 # 等待进程完成，最大超时为 10 秒。
    var jr = r.data    # r.data 的类型为 double
    print jr           # 3.141592 打印
```
```python
    json_parse "{\"test\": \"value\"}" # 双引号必须在 JSON 字符串中进行转义。
    var r = result()
    wait r.status == "finished", 10 # 等待进程完成，最大超时为 10 秒。
    var jr = r.data    # r.data 的类型为 JObject
    print jr           # { _type: "JObject", _sub_file: "", _desc: "", test: "value" } 打印
```