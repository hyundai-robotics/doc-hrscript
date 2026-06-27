# 9.2.1 `load_job`

声明读取 MAIN 模块的 project/jobs/ 文件夹的更改以更新内存。


### 描述

将 MAIN 模块的 project/jobs/ 文件夹中的作业加载到新内存中。

如果您通过 FTP 或 copyfile 命令将 .job 文件复制或覆盖到 jobs/ 文件夹中，则必须执行此语句以反映内存，从而能够选择或调用作业。

- 注意：内存中不存在于 jobs/ 文件夹中的作业将被删除。
- 如果文件的修改时间不同，则会加载该文件。
- 内存中不存在的文件会被加载。

- 由于可以加载大容量 .jobs，因此在后台异步执行，以避免由于加载引起的节拍时间损失。可以通过读取结果变量的值判断加载是否成功完成。
- 当前加载完成之前，无法请求另一个加载。


### 语法

```python
load_job <result-variable>,"*"
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
        后台执行的结果<br>
        <ul>
        <li>1：成功完成。</li>
        <li>0：加载进行中。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">job filename</td>
      <td style="text-align:left">
        您只能使用 "*" 参数，这意味着所有文件。
      </td>
      <td style="text-align:left">字符串表达式</td>
    </tr>
  </tbody>
</table>

### 示例

```python
     var res
     copyfile res,"project/vars","work/vars_1"
     wait res==1,8,*timeout
     copyfile res,"work/sub5.job","project/jobs/0005_sub.job"
     wait res==1,4,*timeout
     load_job res,"*"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "copyfile failed"
     end
```