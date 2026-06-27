# 5.7 `contpath`

### 描述

选择 CONTPATH 的模式。

请参见下面的链接以获取 CONTPATH 的描述。
[操作手册：8.15 R360 手动设置 CONTPATH](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/8-r-code/15-r360?cont_model=${cont_model})

<br><br>


### 语法

```python
contpath <mode number>
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
      <td style="text-align:left">mode number</td>
      <td style="text-align:left">
        0: 不连续<br>
        1: 连续。然而，输入信号是不连续的（默认）<br>
        2: 连续。输入信号也是连续的
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### 示例

```python
contpath 0
contpath 1
contpath 2
```


{% hint style="info" %}

- 如果未明确执行 `contpath` 语句，则默认应用 `contpath 1`。即使明确指定，在周期开始时也会初始化为 `contpath 1`。

- 可以通过标题栏上的 `CP0` / `CP1` / `CP2` 标志检查更改的状态。

{% endhint %}