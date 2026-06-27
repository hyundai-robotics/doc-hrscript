# 9.2.2 `load_csv`

支持从 V60.28-00 开始。

声明将对 MAIN 模块的 `project/vars/` 文件夹中的 .csv 文件（根全局数组）进行内存读取。

### 描述

HRScript 的全局根数组存储在 `vars/` 文件夹中，格式为 CSV 标准格式的文件。（"根" 意味着它不是另一个数组或对象的属性。）

有关变量文件的信息，请参阅以下操作手册链接。

[global variable/variable file](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/6-monitoring/3-job/3-global-variable/3-var-files?cont_model=${cont_model})

您可以使用 PC 上的文本编辑器轻松编辑 .csv 文件。
复制到 `vars/` 文件夹的编辑文件不会立即反映在内存中，而是通过在 TeachPendant 的全局变量窗口中使用 `[load all]` 功能或执行 `load_csv` 语句来实现。

- 由于较大的 .csv 文件可以加载，因此在后台异步执行以避免由于加载而导致的节拍时间损失。通过读取结果变量的值可以确定加载是否成功。
- 当前加载完成之前，不能请求另一个加载。

### 语法

```python
load_csv <result-variable>,"*"
load_csv <result-variable>,"<variable name>"
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
        <li>1: 完成。</li>
        <li>0: 正在加载中。</li>
        </ul>
      </td>
      <td style="text-align:left">变量</td>
    </tr>
    <tr>
      <td style="text-align:left">.csv 文件标题</td>
      <td style="text-align:left">
        <ul>
        <li>"*": 加载所有文件。</li>
        <li>"&lt;variable name&gt;": 加载 &lt;variable name&gt;.csv 文件。</li>
        </ul>
      </td>
      <td style="text-align:left">字符串表达式</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
如果您使用 "*" 加载所有 .csv，则内存中没有 `vars/` 文件夹中的 .csv 的根数组将被删除。
{% endhint %}

### 示例

```python
     var res
     copyfile res,"work/arrs/locs1.csv","project/vars/locs.csv"
     wait res==1,4,*timeout
     load_csv res,"locs"
     wait res==1,4,*timeout
     call 5
     end
     *timeout
     print "加载新位置失败。"
     end
```