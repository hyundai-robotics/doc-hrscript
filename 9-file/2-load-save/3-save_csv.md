# 9.2.3 `save_csv`

支持从 V60.28-00 开始。

声明将全局根数组变量存储到内存中，作为 .csv 文件，位于 MAIN 模块的 `project/vars/` 文件夹中。

### 描述

HRScript 的全局根数组存储在 `vars/` 文件夹中，作为 CSV 标准格式的文件。（“根”意味着它不是另一个数组或对象的属性。）

有关变量文件的信息，请参阅以下操作手册链接。

[global variable/variable file](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/6-monitoring/3-job/3-global-variable/3-var-files?cont_model=${cont_model})

全局根数组并不会在值更改时立即存储到 .csv 文件中。
当你按下 `Ctrl+[F7: save]` 或关闭电源时会将其保存为文件，并且你可以通过执行 `save_csv` 命令立即将其保存为文件。

- 因为可以保存大 .csv 文件，它们在后台异步执行，以避免因保存导致的失去节拍时间。可以通过读取结果变量的值来确定保存是否成功。
- 在当前保存完成之前，无法请求另一次保存。

### 语法

```python
save_csv <result-variable>,"*"
save_csv <result-variable>,"<variable name>"
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
        <li>1: 完成。</li>
        <li>0: 正在保存。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">.csv 文件标题</td>
      <td style="text-align:left">
        <ul>
        <li>"*": 保存所有变量。</li>
        <li>"&lt;variable name&gt;": 保存 &lt;variable name&gt;.csv 文件。</li>
        </ul>
      </td>
      <td style="text-align:left">字符串表达式</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
如果通过指定 "*" 保存所有 .csv， 它不会删除 `vars/` 文件夹中的 .csv 文件，因为对应名称的根变量不存在。
{% endhint %}

### 示例

```python
     var res
     save_csv res,"locs"
     wait res==1,4,*timeout
     copyfile res,"project/vars/locs.csv","work/arrs/locs2.csv"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "failed to save new locations."
     end
```