# 9.1.2 `copyfile`

一个 `copyfile` 是请求复制目录或文件的过程。

### 描述

将指定源路径的目录或文件复制到指定目标路径名。

- 只能在 MAIN 模块中执行，不能在 Teach Pendant 或 USB 存储器中执行。
- 如果目标路径名的中间路径目录不存在，将创建中间路径。
- 如果目标目录已存在，将其删除并复制源目录。
- 如果目标文件已经存在，将覆盖。
- 目录中的所有子目录也会被复制。
- 路径名还支持通配符 ('*', '?')。

- 由于可能复制大文件或整个目录，因此以异步方式在后台执行，以避免因等待复制而导致的节拍时间丢失。换句话说，当执行 `copyfile` 语句时，启动后台任务中的复制，立即继续执行下一个语句。例如，您可以请求复制并执行移动语句。通过读取结果变量的值可以确定复制是否成功完成。(即，在复制失败时不会生成错误或警告。)

- 在一个复制或删除完成之前，您无法请求另一个复制或删除。

### 语法

```python
copyfile <result-variable>,<source pathname>,<destination pathname>
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
        后台执行结果<br>
        <ul>
        <li>1: 成功完成。</li>
        <li>0: 正在复制。</li>
        <li>-1: 源路径名无效。</li>
        <li>-2: 目标路径名无效。</li>
        <li>-3: 复制失败。</li>
        <li>-6: 在复制通配符时全部失败。</li>
        <li>-7: 在复制通配符时部分失败。</li>
        <li>-11: 创建临时路径失败。</li>
<li>-12: 复制到临时路径失败。</li>
<li>-13: 清除现有目标路径失败。</li>
<li>-14: 目标路径创建失败。</li>
<li>-15: 从临时路径移动到目标路径失败。</li>
</ul>
</td>
<td style="text-align:left">变量</td>
</tr>
<tr>
<td style="text-align:left">源路径名</td>
<td style="text-align:left">
要复制的目录路径,<br>
或要复制的文件路径名
</td>
<td style="text-align:left">字符串表达式</td>
</tr>
<tr>
<td style="text-align:left">字符串表达式</td>
<td style="text-align:left">
- 以 '/' 结尾：要复制的路径。<br>
- 不以 '/' 结尾：通过复制将创建的路径名。
</td>
<td style="text-align:left">字符串表达式</td>
</tr>
</tbody>
</table>

### 示例

   var res
   copyfile res,"project/vars","work/vars_1" # vars_1/ 文件夹被创建。
   wait res==1,8,*timeout
   copyfile res,"project/vars","work/vars_1/" # vars_1/vars/ 文件夹被创建。
   wait res==1,8,*timeout
   copyfile res,"work/clear.job","project/jobs/0005_clear.job"
   wait res==1,4,*timeout
   copyfile res,"work/*_sub.job","project/jobs/" # 通配符
   wait res==1,4,*timeout
   call 5
   end
   *timeout
   print "copyfile 失败"
   end
![](../../_assets/copyfile.png)