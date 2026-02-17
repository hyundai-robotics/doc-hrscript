# recv

### 描述

调用 `Sci` 的 `recv` 以接收字符串。

### 语法

&lt;Sci object&gt;.recv string variable \[,{timeout}\] \[,{goto address}\]

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">项目</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">其他</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>string variable</td>
      <td>
        一个字符串变量，当成功接收输入的字符串时将其存放在此处。<br>
      </td>
      <td></td>
    </tr>
    <tr>
      <td>timeout</td>
      <td>
        当指定时间内没有接收到数据时，分支到goto地址，如果没有goto地址，则会发生错误。<br>
        如果未指定，则无限期等待。
      </td>
      <td>毫秒</td>
    </tr>
    <tr>
      <td>goto address</td>
      <td>
        当发生超时时要分支的地址。<br>
        如果未指定，则会停止并发生错误。
      </td>
      <td>地址</td>
    </tr>
  </tbody>
</table>
### 示例

```python
   var msg
   sci2.recv msg,5000,*timeout
   print msg
   ...
   ...
   *timeout
   print "超时错误"
   stop
```