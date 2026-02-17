# 9.1.3 `delfile`

`delfile` 是一个请求删除目录或文件的过程。

### 描述

在指定路径中删除目录或文件。

- 仅能在 MAIN 模块内执行，而不能在 Teach Pendant 或 USB 存储器中执行。
- 目录中的所有子目录也会被删除。
- 如果指定的路径名不存在，则以成功结束。
- 路径名也支持通配符 ('*', '?')。

- 由于可能会删除大的文件或整个目录，因此它在后台异步执行，以避免因等待删除而导致的节拍时间损失。可以通过读取结果变量的值来确定删除是否成功完成。（也就是说，当删除失败时，不会生成错误或警告。）

- 在一份复制或删除完成之前，您不能请求另一个复制或删除。

### 语法

```python
delfile <result-variable>,<pathname>
```

### 参数

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">描述</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result-variable</td>
      <td style="text-align:left">
        背景执行的结果<br>
        <ul>
        <li>1: 成功完成。</li>
        <li>0: 删除正在进行中。</li>
        <li>-41: 删除目录失败。</li>
        <li>-42: 删除文件失败。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">pathname</td>
<td style="text-align:left">
        要删除的目录路径,<br>
        或要删除的文件路径
      </td>
      <td style="text-align:left">字符串表达式</td>
    </tr>
  </tbody>
</table>

### 示例

```python
   var res
   delfile res,"work/vars_1"
   wait res==1,8,*timeout
   delfile res,"work2/10??.job" # wildcard
   wait res==1,8,*timeout
   copyfile res,"project/jobs/0005_sub.job"
   wait res==1,4,*timeout
   end
   *timeout
   print "delfile failed"
   end
```