# recv

### Description

调用 `Sci` 的 `recv` 以接收字符串。

### Syntax

&lt;Sci object&gt;.recv string variable \[,{timeout}\] \[,{goto address}\]

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Item</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Etc</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>string variable</td>
      <td>
        成功接收到的字符串将会存储在此字符串变量中。<br>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>timeout</td>
      <td>
        当在指定时间内未接收到数据时，将跳转到 goto 地址，如果没有 goto 地址，则会发生错误。<br>
        如果未指定，将无限期等待。
      </td>
      <td>msec</td>
    </tr>
    <tr>
      <td>goto address</td>
      <td>
        当发生超时时跳转的地址。<br>
        如果未指定，将以错误停止。
      </td>
      <td>address</td>
    </tr>
  </tbody>
</table>

### Example

```python
   var msg
   sci2.recv msg,5000,*timeout
   print msg
   ...
   ...
   *timeout
   print "timeout error"
   stop
```