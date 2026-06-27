# 10.1.1 `gather`

`gather` 是指定数据收集功能开始和结束的过程。

### 描述

使用 `gather` 指定收集的开始和结束。收集结果文件保存如下；
- 存储路径：MAIN/project
- 文件名：0001.GDT 到 0030.GDT

最多存储 30 个收集结果文件，如果数量超出，则将覆盖先前的收集结果文件。

`gather_state()` 函数返回当前数据收集操作的状态。
  - 0 : 不在收集中。
  - 1 : 在收集中。 (gather 1 ~ gather 0)
  - 2 : 正在将收集结果保存为文件。 (gather 0~)

### 语法

```python
gather <start/end>
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
      <td style="text-align:left">start/end</td>
      <td style="text-align:left">
        <ul>
        <li>1: 数据收集开始</li>
        <li>0: 数据收集结束</li>
        </ul>
      </td>
      <td style="text-align:left">算术表达式</td>
    </tr>
  </tbody>
</table>

### 示例

```python
S1   move L,spd=100%,accu=0,tool=0
     gather 1
S2   move L,spd=100%,accu=0,tool=0
     delay 1.5
S3   move L,spd=100%,accu=0,tool=0
     gather 0
     end
```