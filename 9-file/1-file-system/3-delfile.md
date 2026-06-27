# 9.1.3 `delfile`

A `delfile` 是一个请求删除目录或文件的过程。

### Description

在指定路径中删除目录或文件。

- 只能在 MAIN 模块内执行，不能在 Teach Pendant 或 USB 内存中执行。
- 目录中的所有子目录也会被删除。
- 如果指定的路径不存在，操作成功结束。
- 路径名还支持通配符 ('*', '?')。

- 因为可能会删除大文件或整个目录，所以它在后台异步进行，以避免在删除期间由于等待而导致的触发时间损失。可以通过读取结果变量的值来确定删除是否成功完成。 （即，当删除失败时，不会生成错误或警告。）

- 在一个复制或删除完成之前，你不能请求另一个复制或删除。

### Syntax

```python
delfile <result-variable>,<pathname>
```

### Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">result-variable</td>
      <td style="text-align:left">
        背景执行的结果<br>
        <ul>
        <li>1: 成功完成。</li>
        <li>0: 删除进行中。</li>
        <li>-41: 删除目录失败。</li>
        <li>-42: 删除文件失败。</li>
        </ul>
      </td>
      <td style="text-align:left">variable</td>
    </tr>
    <tr>
      <td style="text-align:left">pathname</td>
      <td style="text-align:left">
        要删除的目录路径，<br>
        或要删除的文件路径
      </td>
      <td style="text-align:left">string expression</td>
    </tr>
  </tbody>
</table>

### Sample

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